# grammar agent

## default

```timeout
20000
```

```execute
echo 'One of \"the most important\" issue is the lack of parking spaces at the local mall.' | aux4 grammar fix --save=out.txt
```

```expect
One of "the most important" issues is the lack of parking spaces at the local mall.
```

## custom config

### custom config with existing model

```file:config.yaml
config:
  grammar:
    model:
      type: openai
      config:
        model: o4-mini
```

```execute
echo 'One of \"the most important\" issue is the lack of parking spaces at the local mall.' | aux4 grammar fix --configFile config.yaml
```

```expect
One of the most important issues is the lack of parking spaces at the local mall.
```

### custom config with non-existing model

```file:config.yaml
config:
  grammar:
    model:
      type: openai
      config:
        model: gpt-WRONG-MODEL
```

```execute
echo 'One of \"the most important\" issue is the lack of parking spaces at the local mall.' | aux4 grammar fix --configFile config.yaml
```

```expect:partial
The model `gpt-WRONG-MODEL` does not exist
```
