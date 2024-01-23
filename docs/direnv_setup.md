
# direnv Installation and Usage Guide

This guide provides detailed instructions on how to install and use `direnv` on an Ubuntu 20.04 system.

## Step 1: Install direnv

### Update Package Lists
Before installing new software, update your package lists.

```bash
sudo apt update
```

### Install direnv
Install `direnv` using `apt`.

```bash
sudo apt install direnv
```

## Step 2: Hook direnv into Your Shell

`direnv` needs to be hooked into your shell to work correctly.

### Open .bashrc
Open your `.bashrc` file in a text editor (like nano).

```bash
nano ~/.bashrc
```

### Add direnv Hook
At the end of the `.bashrc` file, add the following line:

```bash
eval "$(direnv hook bash)"
```

### Save and Exit
Save the file and exit the editor. In nano, press Ctrl + O, Enter to save, and Ctrl + X to exit.

### Reload .bashrc
Reload your `.bashrc` to apply the changes.

```bash
source ~/.bashrc
```

## Step 3: Using direnv

Now, you can start using `direnv`.

### Create an .envrc File
In the root of your project directory, create an `.envrc` file.

```bash
cd /path/to/your/project
nano .envrc
```

### Add Environment Variables
Add your environment variables in key-value pairs in the `.envrc` file. For example:

```bash
export API_KEY="your-api-key"
export DB_PASSWORD="your-db-password"
```

### Save and Exit the Editor
Save and close the file after adding your variables.

### Allow direnv
The first time you modify an `.envrc` in a directory, you need to allow `direnv` to load it.

```bash
direnv allow .
```

### Verify
To verify that `direnv` is loading and unloading your environment correctly, move in and out of your directory.

```bash
echo $API_KEY  # Should show the value inside the directory
cd ..          # Move out of the directory
echo $API_KEY  # Should not show the value outside
```

Congratulations! You've successfully set up `direnv` on your Ubuntu 20.04 system. Remember, after modifying `.envrc`, you need to run `direnv allow .` to approve the changes.