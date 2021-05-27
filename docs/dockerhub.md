## Documentation

Visit us

[https://docs.kics.io](https://docs.kics.io)

## Git Repo

https://github.com/Checkmarx/kics

## Command

To scan a directory/file on your host you have to mount it as a volume to the container and specify the path on the container filesystem with the -p KICS parameter (see the full list of CLI options below)

NOTE: from v1.3.0 KICS does not execute `scan` command by default anymore.


```sh
docker pull checkmarx/kics:latest
```

Scan a directory
```sh
docker run -v {path_to_host_folder_to_scan}:/path checkmarx/kics:latest scan -p "/path" -o "/path/results.json"
```
Scan a single file
```sh
docker run -v {path_to_host_folder}/{filename}.{extention}:/path/{filename}.{extention} checkmarx/kics:latest scan -p "/path" -o "/path/results.json"
```

## CLI Options

Usage:

```txt
Keeping Infrastructure as Code Secure

Usage:
  kics [command]

Available Commands:
  generate-id    Generates uuid for query
  help           Help about any command
  list-platforms List supported platforms
  scan           Executes a scan analysis
  version        Displays the current version

Flags:
      --ci                  display only log messages to CLI output (mutually exclusive with silent)
  -h, --help                help for kics
  -f, --log-format string   determines log format (pretty,json) (default "pretty")
      --log-level string    determines log level (TRACE,DEBUG,INFO,WARN,ERROR,FATAL) (default "INFO")
      --log-path string     path to generate log file (info.log)
      --no-color            disable CLI color output
      --profiling string    enables performance profiler that prints resource consumption metrics in the logs during the execution (CPU, MEM)
  -s, --silent              silence stdout messages (mutually exclusive with verbose and ci)
  -v, --verbose             write logs to stdout too (mutually exclusive with silent)

Use "kics [command] --help" for more information about a command.
```

Scan command:

```txt
Executes a scan analysis

Usage:
  kics scan [flags]

Flags:
      --config string                path to configuration file
      --exclude-categories strings   exclude categories by providing its name
                                     can be provided multiple times or as a comma separated string
                                     example: 'Access control,Best practices'
  -e, --exclude-paths strings        exclude paths from scan
                                     supports glob and can be provided multiple times or as a quoted comma separated string
                                     example: './shouldNotScan/*,somefile.txt'
      --exclude-queries strings      exclude queries by providing the query ID
                                     can be provided multiple times or as a comma separated string
                                     example: 'e69890e6-fce5-461d-98ad-cb98318dfc96,4728cd65-a20c-49da-8b31-9c08b423e4db'
  -x, --exclude-results strings      exclude results by providing the similarity ID of a result
                                     can be provided multiple times or as a comma separated string
                                     example: 'fec62a97d569662093dbb9739360942f...,31263s5696620s93dbb973d9360942fc2a...'
      --fail-on strings              which kind of results should return an exit code different from 0
                                     accetps: high, medium, low and info
                                     example: "high,low" (default [high,medium,low,info])
  -h, --help                         help for scan
      --ignore-on-exit string        defines which kind of non-zero exits code should be ignored
                                     accepts: all, results, errors, none
                                     example: if 'results' is set, only engine errors will make KICS exit code different from 0 (default "none")
      --minimal-ui                   simplified version of CLI output
      --no-progress                  hides the progress bar
      --output-name string           name used on report creations (default "results")
  -o, --output-path string           directory path to store reports
  -p, --path strings                 paths or directories to scan
                                     example: "./somepath,somefile.txt"
  -d, --payload-path string          path to store internal representation JSON file
      --preview-lines int            number of lines to be display in CLI results (min: 1, max: 30) (default 3)
  -q, --queries-path string          path to directory with queries (default "./assets/queries")
      --report-formats strings       formats in which the results will be exported (all, json, sarif, html) (default [json])
      --timeout int                  number of seconds the query has to execute before being canceled (default 60)
  -t, --type strings                 case insensitive list of platform types to scan
                                     (Ansible, CloudFormation, Dockerfile, Kubernetes, OpenAPI, Terraform)

Global Flags:
      --ci                  display only log messages to CLI output (mutually exclusive with silent)
  -f, --log-format string   determines log format (pretty,json) (default "pretty")
      --log-level string    determines log level (TRACE,DEBUG,INFO,WARN,ERROR,FATAL) (default "INFO")
      --log-path string     path to generate log file (info.log)
      --no-color            disable CLI color output
      --profiling string    enables performance profiler that prints resource consumption metrics in the logs during the execution (CPU, MEM)
  -s, --silent              silence stdout messages (mutually exclusive with verbose and ci)
  -v, --verbose             write logs to stdout too (mutually exclusive with silent)
```