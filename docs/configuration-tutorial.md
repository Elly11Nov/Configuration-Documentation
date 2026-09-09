# Configure a Voice Application

This tutorial walks through the process of creating a basic JSON configuration for a voice application.

By the end of the tutorial, you will have a configuration containing the application identity, language, audio settings and speech resources.

## Before you start

You will need:

* Access to the application repository
* The name of the voice application
* A supported language and locale
* The appropriate acoustic model
* The grammar resource
* The port required by the application

## Step 1: Create the configuration file

Create a file named:

```text
voice-app.json
```

Store the file in the application's repository.

## Step 2: Define the application

Add the application name and a description.

```json
{
  "topic": "voice-app",
  "description": "Example voice command application."
}
```

The `topic` identifies the target application and is used when the application is referenced by other components.

## Step 3: Set the language

Add the language and locale.

```json
"language": "en-US"
```

Use one of the supported language-locale combinations documented in the configuration reference.

## Step 4: Configure the audio settings

Specify the target sample rate and application port.

```json
"sampleRate": "8000",
"port": "10010"
```

The sample rate must correspond to the sample rate supported by the selected acoustic model.

## Step 5: Add the acoustic model

Specify the location of the acoustic model resource.

```json
"acousticModel": {
  "resourcePath": "s3://example-data/models/en-US/acoustic-model"
}
```

## Step 6: Add the grammar

Specify the grammar resource used by the application.

```json
"grammar": {
  "resourcePath": "s3://example-data/grammars/en-US/example-grammar.grxml"
}
```

## Step 7: Review the configuration

The completed configuration should look similar to:

```json
{
  "topic": "voice-app",
  "language": "en-US",
  "sampleRate": "8000",
  "port": "10010",
  "description": "Example voice command application.",
  "acousticModel": {
    "resourcePath": "s3://example-data/models/en-US/acoustic-model"
  },
  "grammar": {
    "resourcePath": "s3://example-data/grammars/en-US/example-grammar.grxml"
  }
}
```

Before committing the file, check that:

* All required parameters are present.
* The language and locale are supported.
* The sample rate matches the acoustic model.
* The resource paths are correct.
* The JSON is valid.

## Step 8: Commit the changes

Commit the configuration to the repository and push the changes.

The application's automated workflow can then process the updated configuration.

## Next steps

For a complete description of the available parameters, see the [Configuration Reference](configuration-reference.md).

