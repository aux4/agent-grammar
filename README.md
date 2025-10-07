# agent/grammar

An AI agent to fix grammar issues in text input.

agent/grammar provides a simple CLI wrapper that corrects and improves English text. It reads text from stdin, applies grammar fixes and clarity improvements using the configured AI model, and writes the corrected text to stdout or an optional file. It's designed for quick, scriptable grammar fixes in pipelines, CI checks, content editing, and bulk-processing tasks.

This package integrates with the aux4 ecosystem and can leverage shared AI agent packages (for example, aux4/ai-agent) to run the underlying model. Key benefits include a consistent CLI interface, configurable model selection via a config file, and an option to save corrected output directly to a file for automation.

## Installation

```bash
aux4 aux4 pkger install agent/grammar
```

## Quick Start

Fix a short sentence from stdin and print the corrected text:

```bash
echo 'One of "the most important" issue is the lack of parking spaces at the local mall.' | aux4 grammar fix
```

This will output the corrected sentence:
One of "the most important" issues is the lack of parking spaces at the local mall.

## Fix grammar from stdin

Use this command to correct grammar of any text provided on stdin. The agent preserves formatting and markdown structure while applying grammar and clarity improvements.

- Command reference: [aux4 grammar fix](./commands/grammar/fix)

Example:

```bash
cat local-test/sent.txt | aux4 grammar fix
```

This reads the file `local-test/sent.txt`, sends it to the grammar agent, and prints the corrected result to stdout.

## Save corrected output to a file

You can save the corrected output to a file using the --save variable. When provided, the agent writes the corrected text to the specified path.

- Command reference: [aux4 grammar fix](./commands/grammar/fix)

Example:

```bash
cat test/input2.txt | aux4 grammar fix --save output.txt && cat output.txt
```

This will save the corrected text into `output.txt` and then print its contents. The `--save` variable is optional; if omitted, corrected text is printed to stdout.

## Use a custom configuration (select model/options)

The agent accepts a configuration file to control which model and settings are used. Provide a YAML file via --configFile to override the package default.

- Command reference: [aux4 grammar fix](./commands/grammar/fix)

Example config (config.yaml):

```yaml
config:
  grammar:
    model:
      type: openai
      config:
        model: o4-mini
```

Example command using that config:

```bash
echo 'One of "the most important" issue is the lack of parking spaces at the local mall.' | aux4 grammar fix --configFile config.yaml
```

If the configured model does not exist or is unavailable, the agent will report an error indicating the missing model (for example: The model `gpt-WRONG-MODEL` does not exist).

## Examples

### Fix grammar issues (simple paragraph)

Problem: Correct common grammar issues in a short paragraph.

Input:

```text
One of the most important issue is the lack of parking spaces at the local mall.
If you don’t mind, I’d prefer leave early tomorrow.
Do you have a few minutes to discuss about this project?
Although I’ve known him for a while, I still can’t believe how much stubborn he is.
Would you like to take part of this activity?
```

Command:

```bash
cat input.txt | aux4 grammar fix
```

Output:

```text
One of the most important issues is the lack of parking spaces at the local mall.
If you don't mind, I'd prefer to leave early tomorrow.
Do you have a few minutes to discuss this project?
Although I've known him for a while, I still can't believe how stubborn he is.
Would you like to take part in this activity?
```

### Fix grammar and save to file

Problem: Save corrected output to disk for later processing.

Input (input2.txt):

```text
She don't like going to the gym on weekends.
The team are working hardly to meet the deadline.
```

Command:

```bash
cat input2.txt | aux4 grammar fix --save output.txt && cat output.txt
```

Output:

```text
She doesn't like going to the gym on weekends.
The team is working hard to meet the deadline.
She doesn't like going to the gym on weekends.
The team is working hard to meet the deadline.
```

### Use a custom model via config file

Problem: Use an alternative model defined in a YAML config.

Config (config.yaml):

```yaml
config:
  grammar:
    model:
      type: openai
      config:
        model: o4-mini
```

Command:

```bash
echo 'One of "the most important" issue is the lack of parking spaces at the local mall.' | aux4 grammar fix --configFile config.yaml
```

Output:

```text
One of the most important issues is the lack of parking spaces at the local mall.
```

If the model named in the config does not exist, the command will return an error message indicating the missing model.

## Configuration

This package reads an optional configuration YAML to control the grammar agent behavior (model selection and provider configuration). The config structure follows:

```yaml
config:
  grammar:
    model:
      type: openai
      config:
        model: <model-name>
```

Use --configFile <path> to point the agent to a different configuration file:

```bash
aux4 grammar fix --configFile config.yaml
```

Configuration is useful for switching models, providers, or fine-tuning provider-specific settings.

## Variables

The grammar fix command accepts these variables:

- configFile (string, optional) — Path to a configuration YAML file. Default: empty (uses package default config).
- save (string, optional) — File path to save the corrected output. Default: empty (prints to stdout).

## License

This package is licensed under the Apache License, Version 2.0.

See [LICENSE](./license) for details.
