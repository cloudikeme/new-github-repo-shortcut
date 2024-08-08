# How to  create a bash shortcut (also known as an alias) to streamline your GitHub repository creation

In this previous post i broke down how to create a bash shortcut also known as an alias. But an Alias has its use cases and limitations especially when its a command that involves giving arguments.One such example is when i wanted to create this shortcut for creating new remote github repos faster using the command line(terminal). I kept getting the erro below:
In such cases you must use a bash function instead. 

Here's how you can create a bash function called `newgithubrepo` to create a GitHub repository:

```bash
newgithubrepo() {
  if [ $# -gt 1 ]; then 
    echo "Error: This function accepts at most 1 argument (the repository name)."
    return 1 # Indicate an error
  fi

  local repo_name="$1"

  gh repo create "$repo_name" --public --source=. --remote=upstream
}
```

**Explanation:**

1. **Function Definition:**
   - `newgithubrepo() { ... }`: This defines a function named `newgithubrepo`.

2. **Argument Check:**
   - `if [ $# -gt 1 ]; then ... fi`: This checks if the number of arguments passed to the function (`$#`) is greater than 1. If so, it prints an error message and exits the function using `return 1` (which signals an error).

3. **Repository Name:**
   - `local repo_name="$1"`: This line stores the first argument passed to the function (which should be the repository name) into the `repo_name` variable. The `local` keyword ensures the variable is only available within the function's scope.

4. **GitHub CLI Command:**
   - `gh repo create "$repo_name" --public --source=. --remote=upstream`: This is the same `gh` command you used before, now using the `repo_name` variable.

**How to Use the Function:**

1. **Add the function** to your `.bashrc` file (or create a separate shell script if you prefer).
2. **Source your `.bashrc`:** `source ~/.bashrc`
3. **Call the function:**
   ```bash
   newgithubrepo my-awesome-project
   ```

**Advantages of Using a Function:**

- **Error Handling:** The function now includes a check for the correct number of arguments, making it more robust.
- **Readability:** Functions often improve the readability and organization of your code, especially for more complex tasks. 
- **Reusability:**  You can easily call the function multiple times with different repository names.

Let me know if you'd like to add any more features or customizations to your function! 

Here's how you can create a bash shortcut (also known as an alias) to streamline your GitHub repository creation:

**1. Open Your Bash Aliases File**

   WARNING! avoid  editing or configuring your .bashrc profile if it can be avoided , so you dont break your bash profile. When it comes to aliases and bash shortcuts a safer way i advice is to create and always use a Bash Aliases file. 
   
   Open your terminal and use a text editor like nano to edit your `.bash_aliases` file:

   ```bash
  sudo nano ~/.bash_aliases
   ```

**2. Add the Alias**

   At the end of your `.bash_aliases` file, add the following line:

   ```bash
   alias newgithubrepo='gh repo create "$1" --public --source=. --remote=upstream'
   ```

   **Explanation:**

   - **`alias newgithubrepo='...'`**: This creates a new command called `newgithubrepo`. Feel free to choose a different name for your alias if you prefer.
   - **`gh repo create "$1" ...`**: This is the core GitHub command. The `"$1"` means it will take the first argument you provide after the alias and use it as the repository name. 
   - **`--public`**: Makes the repository public.
   - **`--source=.`**:  Uses your current directory as the source for the repository.
   - **`--remote=upstream`**: Sets up the `upstream` remote, which is a common convention for tracking the original repository you forked from (if applicable).

**3. Save and Reload**

   - Save the changes to your `.bashrc` file (Ctrl+X, then Y, then Enter in `nano`).
   - Reload your bash profile by running: 
     ```bash
     source ~/.bashrc 
     ```

**4. Usage**

   Now you can create a new GitHub repository like this:

   ```bash
   newgithubrepo my-awesome-project
   ```

   This will create a public GitHub repository named "my-awesome-project", using your current directory as the source and setting up the `upstream` remote. 

**Key Points and Customization:**

- **Naming:**  Choose a memorable name for your alias.
- **Private Repositories:** To create private repositories, remove the `--public` flag from the alias definition.
- **Remote Naming:** You can customize the remote name (e.g., `--remote=origin`) if needed.

Let me know if you have any more questions or would like to explore further customizations! 
