# STRUCT: Automated Project Structure Generator

![Struct Banner](extras/banner.png)

> ⚠️ **Warning:** This project is still in development and may contain bugs. Use it at your own risk.

STRUCT is a powerful and flexible script designed to automate the creation of project structures based on YAML configurations. It supports template variables, custom file permissions, remote content fetching, and multiple file handling strategies to streamline your development setup process.

## Features

- **YAML Configuration**: Define your project structure in a simple YAML file.
- **Template Variables**: Use placeholders in your configuration and replace them with actual values at runtime.
- **Custom File Permissions**: Set custom permissions for your files directly from the YAML configuration.
- **Remote Content Fetching**: Include content from remote files by specifying their URLs.
- **File Handling Strategies**: Choose from multiple strategies (overwrite, skip, append, rename, backup) to manage existing files.
- **Dry Run**: Preview the actions without making any changes to your file system.
- **Configuration Validation**: Ensure your YAML configuration is valid before executing the script.
- **Verbose Logging**: Get detailed logs of the script's actions for easy debugging and monitoring.

## Installation

You can install STRUCT using pip:

```sh
pip install git+https://github.com/httpdss/struct.git
```

Alternatively, you can clone the repository and install it locally. see the [Development](#development) section for more details.

## Quick Start using Docker

You can run STRUCT using Docker without installing it on your system. Here's how you can do it:

1. Create a YAML configuration file for your project structure. See sample configuration [here](./example/structure.yaml).
2. Run the following command to generate the project structure:

```sh
docker run \
  -v $(pwd):/workdir \
  -e OPENAI_API_KEY=your-key \
  ghcr.io/httpdss/struct:main \
  /workdir/structure.yaml \
  .
```

## Usage

Run the script with the following command:

- OPTIONS which are optional
- First argument is the file where project structure is defined
- Second argument is the path where the project structure will be created

```sh
usage: struct [-h] [--log LOG] [--dry-run] [--vars VARS] [--backup BACKUP] [--file-strategy {overwrite,skip,append,rename,backup}] [--log-file LOG_FILE] yaml_file base_path
```

### Options

- `-h` or `--help`: Show help and exit
- `--log`: Set the logging level (DEBUG, INFO, WARNING, ERROR, CRITICAL). Default is INFO.
- `--dry-run`: Perform a dry run without creating any files or directories.
- `--vars`: Template variables in the format `KEY1=value1,KEY2=value2`.
- `--backup`: Path to the backup folder.
- `--file-strategy`: Strategy for handling existing files (overwrite, skip, append, rename, backup). Default is overwrite.
- `--log-file`: Path to a log file.

### Example

```sh
struct \
  --log=DEBUG \
  --dry-run \
  --vars="project_name=MyProject,author_name=JohnDoe" \
  --backup=/path/to/backup \
  --file-strategy=rename \
  --log-file=/path/to/logfile.log \
  ./example/structure.yaml \
  /path/to/your/output/directory
```

## YAML Configuration

Here is an example of a YAML configuration file:

```yaml
structure:
  - README.md:
      content: |
        # ${project_name}
        This is a template repository.
  - script.sh:
      permissions: '0777'
      content: |
        #!/bin/bash
        echo "Hello, ${author_name}!"
  - LICENSE:
      file: https://raw.githubusercontent.com/nishanths/license/master/LICENSE
  - src/main.py:
      content: |
        print("Hello, World!")

```

## Development

To get started with development, follow these steps:

- Clone the repository
- Create a virtual environment

```sh
python3 -m venv .venv
source .venv/bin/activate
```

- Install the dependencies

```sh
pip install -r requirements.txt
pip install -r requirements.dev.txt
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Funding

If you find this project helpful, please consider supporting it through donations: [patreon/structproject](https://patreon.com/structproject)

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

## Acknowledgments

Special thanks to all the contributors who helped make this project possible.
