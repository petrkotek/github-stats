# Introduction

# Usage examples
## Set up
```bash
export GITHUB_USERNAME=username
export GITHUB_PASSWORD=password
```

## Running the script
```bash
php main.php organisation/repository ../repository-path master > pull_request_stats.txt
```

## Processing data
_For simplicity, move `pull_requests_stats.txt` file to the directory where analyzed repository sits._

### List files without pull request
```bash
cat pull_request_stats.txt | grep '^N[[:space:]]' | sed 's/^N[[:space:]]//g' | grep \.php$
```

### Convert indentation (from tabs to spaces) in files without a pull request:
```bash
cat pull_request_stats.txt | grep '^N[[:space:]]' | sed 's/^N[[:space:]]//g' | grep \.php$ > files_to_convert.txt
cat files_to_convert.txt | awk '{print "expand -t 4 ", $0, " > /tmp/e; mv /tmp/e ", $0}' | sh
```
