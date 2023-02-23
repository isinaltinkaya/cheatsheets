# Code safety in bash scripts and snakemake pipelines


## 1. Prefer using the `>` operator over `>>` whenever possible.

The `>` operator overwrites the file with new content, while the `>>` operator appends content to the end of the file.

Using `>>` can lead to collision issues when multiple processes try to append to the same file at the same time. This can potentially lead to corrupted output or data loss. By using `>` to overwrite the file with new content each time, we can avoid these collision issues and ensure that the output is accurate and reliable.

## 2. Listing files in a directory

When listing files in a directory using a command like

```sh
ls some_dir/*fa > output
```

the process is **not deterministic** as it will list all files that exist at the time in the specified directory.


While it may seem safe at first since we created the directory and are writing to it, there are various ways in which users or systems can interfere, such as adding irrelevant or temporary files. This can put us in an unsafe zone.

To ensure code safety in this situation, one solution is to collect the output file names as full paths in a list as we write them, and after all is done, write that list to the output. This way, we can ensure that only the intended files are included and any errors during the file writing process can be caught, such as missing files.


## 3. Consider the cases where output file may already exist

```python
if os.path.exists(dir_out):
    # if output directory exists, check if it is empty
    if os.listdir(dir_out):
        # if not empty, raise an error or handle it in a different way
        raise ValueError(f"Output directory {dir_out} is not empty")
    else:
        ...
else:
    # create the output directory if it does not exist
    os.makedirs(dir_out)
```


In this version, we first check if the output directory already exists using `os.path.exists`. If it does, we check if it is empty by using `os.listdir` to list all files in the directory. If the directory is not empty, we raise a ValueError with a helpful error message. This ensures that the code will not overwrite existing files or cause unexpected behavior. If the output directory does not exist, we create it using `os.makedirs`. By checking for the existence and emptiness of the output directory, we can prevent errors and ensure that the code is safe and predictable.



## 4. Prefer os library functions to string concatenation

Using `os.path.join` to create file paths is a safer and more reliable way to concatenate directory and file names. It is more robust than string concatenation and helps to avoid errors and security issues that can arise when working with file paths. This ensures that the resulting path will be correctly formatted for the operating system being used, e.g. considering if the directory separator is `/` or `\`, or putting `/` instead of `//`.
