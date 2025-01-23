# 9_2_1 Manually instrument your PHP application with OpenTelemetry

## In this tutorial we will instrument PHP application with Opentelemetry using the environment created in 

- install PHP and composer with below commands:
> use root user
```
apt install php -y
apt install unzip
apt install composer
```
> php -v  (checks installation)

- install opentelemetry dependencies with composer  :
> Note DO NOT run composer with root user. Use  Ubuntu user.
```
composer require php-http/guzzle7-adapter
composer require open-telemetry/opentelemetry
composer require open-telemetry/opentelemetry-logger-monolog
```
- Open VS code from your browser and login
- click on extensions icon and install PHP Debug extension

![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/phpdebug.png?raw=true)

- Using VS code create a file otel.php in /home/ubuntu/ directory and copy and paste the below code:
  
- make sure you replace under the // ===== GENERAL SETUP ===== section with your environment ID and your own token
	> $DT_API_URL = 'https://_YOUR_ENVIRONMENT_ID_.live.dynatrace.com/api/v2/otlp';
 
 	> $DT_API_TOKEN = 'YOUR_OWN_TOKEN';
 
```
<?php
	declare(strict_types=1);
	require __DIR__ . '/vendor/autoload.php';

	// ===== OpenTelemetry Imports =====

	use Monolog\Handler\StreamHandler;
	use Monolog\Logger;
	use OpenTelemetry\Contrib\Otlp\OtlpHttpTransportFactory;
	use OpenTelemetry\Contrib\Otlp\SpanExporter;
	use OpenTelemetry\SDK\Sdk;
	use OpenTelemetry\SDK\Trace\SpanProcessor\SimpleSpanProcessor;
	use OpenTelemetry\SDK\Trace\TracerProvider;
	use OpenTelemetry\SDK\Resource\ResourceInfoFactory;
	use OpenTelemetry\SDK\Resource\ResourceInfo;
	use OpenTelemetry\SDK\Common\Attribute\Attributes;
	use OpenTelemetry\API\Trace\Propagation\TraceContextPropagator;
	use OpenTelemetry\SemConv\ResourceAttributes;

	use OpenTelemetry\SDK\Metrics\MeterProvider;
	use OpenTelemetry\Contrib\Otlp\MetricExporter;
	use OpenTelemetry\SDK\Common\Time\ClockFactory;
	use OpenTelemetry\SDK\Metrics\MetricReader\ExportingReader;

	use OpenTelemetry\Contrib\Otlp\LogsExporter;
	use OpenTelemetry\SDK\Logs\LoggerProvider;
	use OpenTelemetry\SDK\Logs\Processor\SimpleLogRecordProcessor;
	use OpenTelemetry\Contrib\Logs\Monolog\Handler;
	use Psr\Log\LogLevel;


	// ===== GENERAL SETUP =====
    
	$DT_API_URL = 'https://<environment ID>.live.dynatrace.com/api/v2/otlp';
	$DT_API_TOKEN = '<YOUR TOKEN>';

	$dtMetadata = [];

	foreach (['/var/lib/dynatrace/enrichment/dt_metadata.properties',
              'dt_metadata_e617c525669e072eebe3d0f08212e8f2.properties',
              '/var/lib/dynatrace/enrichment/dt_host_metadata.properties'] as $filePath) {
		try {
			if (file_exists($filePath)) {
				$props = str_starts_with($filePath, '/var/') ? parse_ini_file($filePath) : parse_ini_file(trim(file_get_contents($filePath)));
				$dtMetadata = array_merge($dtMetadata, $props);
			}
		} catch (Exception $e) {}
	}

	$resource = ResourceInfoFactory::defaultResource()->merge(ResourceInfo::create(Attributes::create([$dtMetadata,
        ResourceAttributes::SERVICE_NAME => 'php-quickstart'])));


	// ===== TRACING SETUP =====

	$transport = (new OtlpHttpTransportFactory())->create($DT_API_URL . '/v1/traces', 'application/x-protobuf', [ 'Authorization' => 'Api-Token ' . $DT_API_TOKEN ]);

	$exporter = new SpanExporter($transport);

	$tracerProvider =  new TracerProvider(new SimpleSpanProcessor($exporter), null, $resource);


	// ===== METRIC SETUP =====

	$reader = new ExportingReader(
		new MetricExporter((new OtlpHttpTransportFactory())->create($DT_API_URL . '/v1/metrics', 'application/x-protobuf', [ 'Authorization' => 'Api-Token ' . $DT_API_TOKEN ])),
		ClockFactory::getDefault()
	);

	$meterProvider = MeterProvider::builder()->setResource($resource)->addReader($reader)->build();


	// ===== LOG SETUP =====

	$transport = (new OtlpHttpTransportFactory())->create($DT_API_URL . '/v1/logs', 'application/x-protobuf', [ 'Authorization' => 'Api-Token ' . $DT_API_TOKEN ]);

	$exporter = new LogsExporter($transport);

	$loggerProvider = LoggerProvider::builder()
		->addLogRecordProcessor(new SimpleLogRecordProcessor($exporter))
		->setResource($resource)
		->build();

	$handler = new Handler($loggerProvider, LogLevel::INFO);

	$monolog = new Logger('example', [$handler]);


	// ===== REGISTRATION =====

	Sdk::builder()
		->setTracerProvider($tracerProvider)
		->setMeterProvider($meterProvider)
		->setLoggerProvider($loggerProvider)
		->setPropagator(TraceContextPropagator::getInstance())
		->setAutoShutdown(true)
		->buildAndRegisterGlobal();
```
![](https://github.com/hakansuku/D1APACTraining/blob/main/images/PHP/otel.png?raw=true)


