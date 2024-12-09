# config
Starter config files to easily add to new projects

Meant to be used with this bash script:
```bash
# Usage: ca <filename> [--output <directory>] [--replace]
# default behavior is to not replace existing files
ca() {
  # Base URL for your GitHub config repository
  local base_url="https://raw.githubusercontent.com/aidansunbury/config/main"

  # Initialize variables
  local file=""
  local output_dir="."
  local replace=false

  # Parse arguments
  while [[ $# -gt 0 ]]; do
    case $1 in
      --output)
        output_dir="$2"
        shift 2
        ;;
      --replace)
        replace=true
        shift
        ;;
      *)
        file="$1"
        shift
        ;;
    esac
  done

  # Check if a filename is provided
  if [ -z "$file" ]; then
    echo "Error: Please specify a filename."
    return 1
  fi

  # Ensure the output directory exists
  mkdir -p "$output_dir"

  # Full path to the output file
  local output_file="${output_dir}/${file}"
  local url="${base_url}/${file}"

  # Check if the file already exists
  if [ -f "$output_file" ] && ! $replace; then
    echo "Error: $output_file already exists. Use --replace to overwrite."
    return 1
  fi

  # Use curl to download the file, and handle errors if it doesn't exist
  if curl -f -o "$output_file" "$url"; then
    echo "$output_file has been downloaded successfully from $url"
  else
    echo "Error: File $file not found at $url."
    return 1
  fi
}
```