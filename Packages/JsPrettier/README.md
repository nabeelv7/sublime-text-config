# JsPrettier

[![ci](https://github.com/jonlabelle/SublimeJsPrettier/actions/workflows/ci.yml/badge.svg?branch=master)](https://github.com/jonlabelle/SublimeJsPrettier/actions/workflows/ci.yml)
[![Package Control Installs](https://img.shields.io/packagecontrol/dt/JsPrettier.svg?label=installs)](https://packagecontrol.io/packages/JsPrettier)
[![Latest Release](https://img.shields.io/github/v/tag/jonlabelle/SublimeJsPrettier.svg?label=version&sort=semver)](https://github.com/jonlabelle/SublimeJsPrettier/tags)
[![MIT License](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/jonlabelle/SublimeJsPrettier/blob/master/LICENSE)

> [JsPrettier] is a Sublime Text Plugin for [Prettier], the opinionated code
> formatter.

[![Before and After JsPrettier](https://github.com/jonlabelle/SublimeJsPrettier/blob/master/screenshots/before_and_after.gif?raw=true)](https://github.com/jonlabelle/SublimeJsPrettier/blob/master/screenshots/demo.gif)

> [Watch a Quick Demo]

---

<details>
<summary><strong>Table of Contents</strong></summary>

- [Installation](#installation)
    - [Requirements](#requirements)
    - [Install Prettier](#install-prettier)
    - [Install JsPrettier via Package Control](#install-jsprettier-via-package-control)
    - [Install JsPrettier Manually](#install-jsprettier-manually)
    - [Install JsPrettier Using Git](#install-jsprettier-using-git)
- [Usage](#usage)
    - [Command Scope](#command-scope)
- [Plugin Settings and Prettier Options](#plugin-settings-and-prettier-options)
    - [Plugin Settings](#plugin-settings)
    - [Prettier Options](#prettier-options)
    - [Project-level Settings](#project-level-settings)
    - [Prettier Configuration Files](#prettier-configuration-files)
- [Prettier Community Plugins](#prettier-community-plugins)
- [Issues](#issues)
- [Changes](#changes)
- [License](#license)
- [Author](#author)

</details>

## Installation

[JsPrettier] is compatible with both Sublime Text 2 and 3, and all supported
Operating Systems.

### Requirements

- [Sublime Text]
- [Node.js]
    - [npm], [pnpm], or [yarn]
        - [Prettier]

### Install Prettier

If you've already installed [Prettier], you're all set... otherwise:

```bash
# npm (local)
npm install --save-dev prettier

# npm (globally)
npm install --global prettier

# or

# pnpm (local)
pnpm add -D prettier

# pnpm (globally)
pnpm add -g prettier

# or

# yarn (local)
yarn add prettier --dev

# yarn (globally)
yarn global add prettier
```

### Install JsPrettier via Package Control

The recommended way to install JsPrettier is via [Package Control].

From the main application menu:

1. Open the **Tools** Menu
2. Select **Command Palette...**
3. Choose **Package Control: Install Package**
4. Type **JsPrettier** and select it to complete the installation

### Install JsPrettier Manually

1. Download the JsPrettier [zip file] from the GitHub repository.
2. Extract the downloaded zip file.
3. Move the extracted directory to your [Sublime Text Packages directory].
4. Rename the extracted directory from `SublimeJsPrettier-master` to `JsPrettier`.

**Default Sublime Text Packages Paths:** <a name="default-st-paths"></a>

- **OS X:** `~/Library/Application Support/Sublime Text [2|3]/Packages`
- **Linux:** `~/.Sublime Text [2|3]/Packages`
- **Windows:** `%APPDATA%/Sublime Text [2|3]/Packages`

> [!NOTE]  
> Replace the `[2|3]` part with the appropriate Sublime Text version for your
> installation.

### Install JsPrettier Using Git

If you're a Git user, you can install [JsPrettier] and keep it up-to-date by
cloning the repository directly into your [Sublime Text Packages directory].

> **TIP:** You can locate your Sublime Text Packages directory by using the
> application menu `Preferences` -> `Browse Packages...`.

```bash
git clone https://github.com/jonlabelle/SublimeJsPrettier.git "JsPrettier"
```

## Usage

JsPrettier allows you to format your code using Prettier directly within Sublime Text.

There are three available options to format code:

1. **Command Palette:** From the command palette (<kbd>ctrl/cmd + shift + p</kbd>), type **JsPrettier Format Code**.
2. **Context Menu:** Right-click anywhere in the file to bring up the context menu and select **JsPrettier Format Code**.
3. **Key Binding:** There is no default key binding to run Prettier, but here's how to [add your own].

## Command Scope

JsPrettier formats selected code first; if no selection is made, it formats the
entire file. When `auto_format_on_save` is enabled, the entire file will be
formatted on save.

To add a [custom key binding], open the Sublime Text key bindings file by
navigating to `Preferences -> Key Bindings` and add the following configuration:

```json
{ "keys": ["ctrl+alt+f"], "command": "js_prettier" }
```

## Plugin Settings and Prettier Options

Configure plugin settings and Prettier options via the application menu:

- **Preferences**
    - **Package Settings**
        - **JsPrettier**
            - **Settings - Default** (to view the defaults)
            - **Settings - User** (to override the defaults)

### Plugin Settings

- **debug** (default: ***false***)  
    When enabled (*true*), debug info will print to the console - useful for
    troubleshooting and inspecting generated commands passed to Prettier.
    Enabling debug mode also sets Prettier's [`--log-level`] option to `debug`
    (when not overridden by `additional_cli_args`), for printing additional
    debug information to the console.

- **prettier_cli_path** (default: ***empty***)  
    If Sublime Text has problems automatically resolving a path to [Prettier],
    you can set a custom path here. When the setting is empty, the plugin will
    attempt to find Prettier by:

    1. Locally installed prettier relative to active view.
    2. Locally installed prettier relative to the Sublime Text Project file's root directory.
    3. The current user home directory.
    4. JsPrettier Sublime Text plugin directory.
    5. Globally installed prettier.
  
    **Examples:**
  
    ```jsonc
    {
        // macOS and Linux examples:
        "prettier_cli_path": "/usr/local/bin/prettier",
        "prettier_cli_path": "/some/absolute/path/to/node_modules/.bin/prettier",
        "prettier_cli_path": "./node_modules/.bin/prettier",
        "prettier_cli_path": "~/bin/prettier",
        "prettier_cli_path": "$HOME/bin/prettier",
        "prettier_cli_path": "${project_path}/bin/prettier",
        "prettier_cli_path": "$ENV/bin/prettier",
        "prettier_cli_path": "$NVM_BIN/prettier",

        // Windows examples:
        "prettier_cli_path": "C:/path/to/prettier.cmd",
        "prettier_cli_path": "%USERPROFILE%\\bin\\prettier.cmd"
    }
    ```

- **node_path** (default: ***empty***)  
    If Sublime Text has problems resolving the absolute path to node, you can
    set a custom path here.
  
    **Examples:**
  
    ```jsonc
    {
        // macOS/Linux:
        "node_path": "/usr/local/bin/node",
        "node_path": "/some/absolute/path/to/node",
        "node_path": "./node",
        "node_path": "~/bin/node",
        "node_path": "$HOME/bin/node",
        "node_path": "${project_path}/bin/node",
        "node_path": "$ENV/bin/node",
        "node_path": "$NVM_BIN/node",

        // Windows:
        "node_path": "C:/path/to/node.exe",
        "node_path": "%USERPROFILE%\\bin\\node.exe"
    }
    ```

- **auto_format_on_save** (default: ***false***)  
    Automatically format the file on save.

- **auto_format_on_save_excludes** (default: [])  
    File exclusion patterns to ignore when `auto_format_on_save` is enabled.
  
    **Example:**
  
    ```json
    {
        "auto_format_on_save_excludes": [
            "*/node_modules/*",
            "*/file.js",
            "*.json"
        ]
    }
    ```

- **auto_format_on_save_requires_prettier_config** (default: ***false***)  
    Enable auto format on save *only* when a Prettier config file is (or isn't)
    found.

    The Prettier config file is resolved by first checking if a `--config </path/to/prettier/config>`
    is specified in the `additional_cli_args` setting, then by searching the
    location of the file being formatted, and finally navigating up the file tree
    until a config file is (or isn't) found.

- **allow_inline_formatting** (default: ***false***)  
    Enables the ability to format *selections* of in-lined code. For example, to
    format a selection of JavaScript code within a PHP or HTML file. When
    ***true***, the JsPrettier command is available for use across all Sublime
    Text syntaxes.

- **custom_file_extensions** (default: [])  
    There's built-in support already for `js`, `jsx`, `cjs`, `mjs`, `json`,
    `jsonc`, `json5`, `html`, `graphql/gql`, `ts`, `tsx`, `cts`, `mts`, `css`,
    `scss`, `less`, `md`, `mdx`, `yml`, `yaml`, `vue` and `component.html`
    (angular html) files.

    Put additional file extensions here, and be sure not to include the
    leading dot in the file extension.

- **max_file_size_limit** (default: ***-1***)  
    The max allowed file size to format in bytes. For performance reasons,
    files with a greater file size than the specified `max_file_size_limit` will
    not format. Setting the `max_file_size_limit` value to ***-1*** disables the
    file size checking (default).

- **disable_tab_width_auto_detection** (default: ***false***)  
    Whether or not to disable the plugin from automatically setting Prettier's
    [--tab-width](https://prettier.io/docs/en/options.html#tab-width)
    option, and adhere to the Prettier configured setting.

- **disable_prettier_cursor_offset** (default: ***false***)  
    There's an apparent (and nasty) defect in Prettier that seems to occur
    during Prettier's [cursor offset](https://prettier.io/docs/en/api.html#prettierformatwithcursorsource--options)
    calculation, and when attempting to format large or minimized files (but not limited to just these cases).
    The issue effectively results in the CPU spiking to a constant 100%...
    indefinitely, or until the node executable/process running Prettier is
    forcefully terminated.

    To avoid this problematic behavior, or until the defect is resolved, you can
    disable the plugin (JsPrettier) from ever passing the cursor offset
    position to Prettier by setting the `disable_prettier_cursor_offset` value
    to `true`.

    - See related issues: [#147](https://github.com/jonlabelle/SublimeJsPrettier/issues/147), [#168](https://github.com/jonlabelle/SublimeJsPrettier/issues/168)
    - [Prettier Cursor Offset Documentation](https://prettier.io/docs/en/api.html#prettierformatwithcursorsource--options)

- **additional_cli_args** (default: {})  
    A key-value pair of arguments to append to the prettier command.

    **Examples:**

    ```jsonc
    {
        "additional_cli_args": {
            "--config": "~/.prettierrc",
            // or
            "--config": "$HOME/.prettierrc",
            // or
            "--config": "${project_path}/.prettierrc",
            // or
            "--config": "/some/absolute/path/to/.prettierrc",

            "--config-precedence": "file-override",
            "--ignore-path": "${file_path}/.prettierignore",
            "--with-node-modules": "",
            "--plugin-search-dir": "$folder"
        }
    }
    ```

### Prettier Options

- **useTabs** (internally set by the [***translate_tabs_to_spaces***] setting)  
    Indent lines with tabs.

- **printWidth** (default: ***80***)  
    Specifies that the formatted code should fit within this line limit.

- **tabWidth**  (default: ***2***)  
    Specify the number of spaces per indentation-level.

    **IMPORTANT:** By default, "tabWidth" is automatically set using the
    SublimeText configured value for "[tab_size]". To disable this behavior, you
    must first change the `disable_tab_width_auto_detection` value from `false`,
    to `true`.

- **singleQuote** (default: ***false***)  
    Format code using single or double-quotes.

- **trailingComma** (default: "***all***")  
   Controls the printing of trailing commas wherever possible. Valid options:
    - "***none***" - No trailing commas
    - "***es5***" - Trailing commas where valid in ES5 (objects, arrays, etc)
    - "***all***" - Trailing commas wherever possible (function arguments)

- **bracketSpacing** (default: ***true***)  
    Controls the printing of spaces inside object literals.

- **bracketSameLine** (default: ***false***)  
    Put the `>` of a multi-line HTML (HTML, JSX, Vue, Angular) element at the
    end of the last line instead of being alone on the next line
    (does not apply to self closing elements).

- **jsxSingleQuote** (default: ***false***)  
    Use single quotes instead of double quotes in JSX.
  
- **semi** (default: ***true***)  
    ***true*** to add a semicolon at the end of every line, or ***false*** to
    add a semicolon at the beginning of lines that may introduce ASI failures.

- **requirePragma** (default: ***false***)  
    Prettier can ignore formatting files that contain a special comment, called
    a *pragma* at the top of the file. This is useful when gradually
    transitioning large, unformatted codebases to prettier.

    For example, a file with its first comment specified below, and the
    `--require-pragma` option:

    ```javascript
    /**
     * @prettier
     */
    ```

    or

    ```javascript
    /**
     * @format
     */
    ```

- **proseWrap** (default: "***preserve***")  
    (*Markdown and YAML Only*) By default, Prettier will wrap Markdown and YAML
    text as-is since some services use a linebreak-sensitive renderer, e.g.
    GitHub comment and BitBucket. In some cases you may want to rely on
    SublimeText soft wrapping instead, so this option allows you to opt out with
    "never".

    Valid Options:

    - "***always***" - Wrap prose if it exceeds the print width.
    - "***never***" - Do not wrap prose.
    - "***preserve***" (default) - Wrap prose as-is. available in v1.9.0+

- **arrowParens** (default: "***always***")  
    Include parentheses around a sole arrow function parameter.

    Valid Options:

    - "***avoid***" - Omit parentheses when possible. Example: `x => x`
    - "***always***" (always) - Always include parentheses. Example: `(x) => x`

- **htmlWhitespaceSensitivity** (default: "***css***")  
    (*HTML Only*) Specify the global whitespace sensitivity for HTML files,
    see [whitespace-sensitive formatting] for more info.

    Valid Options:

    - "***css***" (default) - Respect the default value of CSS display property.
    - "***strict***" - Whitespaces are considered sensitive.
    - "***ignore***" - Whitespaces are considered insensitive.

- **quoteProps** (default: "***as-needed***")  
    Change when properties in objects are quoted. Requires [Prettier v1.17+].

    Valid options:

    - "***as-needed***" (default) - Only add quotes around object properties where required.
    - "***consistent***" - If at least one property in an object requires quotes, quote all properties.
    - "***preserve***" - Respect the input use of quotes in object properties.

- **vueIndentScriptAndStyle** (default: ***false***)  
    (*Vue files Only*) Whether or not to indent the code inside `<script>`
    and `<style>` tags in Vue files. Some people (like [the creator of Vue](https://github.com/prettier/prettier/issues/3888#issuecomment-459521863))
    don't indent to save an indentation level, but this might break code
    folding in Sublime Text.

    Valid Options:

    - ***false*** (default) - Do not indent script and style tags in Vue files.
    - ***true*** - Indent script and style tags in Vue files.

- **embeddedLanguageFormatting** (default: "***auto***")  
    Control whether Prettier formats quoted code embedded in the file.

    When Prettier identifies cases where it looks like you've placed some code
    it knows how to format within a string in another file, like in a tagged
    template in JavaScript with a tag named `html` or in code blocks in
    Markdown, it will by default try to format that code.

    Sometimes this behavior is undesirable, particularly in cases where you
    might not have intended the string to be interpreted as code. This option
    allows you to switch between the default behavior (`auto`) and disabling
    this feature entirely (`off`).

    See [example](https://prettier.io/blog/2020/08/24/2.1.0.html#add---embedded-language-formattingautooff-option-7875httpsgithubcomprettierprettierpull7875-by-bakkothttpsgithubcombakkot-8825httpsgithubcomprettierprettierpull8825-by-fiskerhttpsgithubcomfiskers).

    Valid Options:

    - "***auto***" (default) - Format embedded code if Prettier can automatically identify it.
    - "***off***" - Never automatically format embedded code.

- **editorconfig** (default: ***true***)  
    Whether to take into account [\.editorconfig] files when parsing configuration.

    If `editorconfig` is `true` and an .editorconfig file is in your project,
    Prettier will parse it and convert its properties to the corresponding
    Prettier configuration. This configuration will be overridden by
    .prettierrc, etc. Currently, the following EditorConfig properties
    are supported:

    - `end_of_line`
    - `indent_style`
    - `indent_size/tab_width`
    - `max_line_length`

- **singleAttributePerLine** (default: ***false***)  
    Enforce single attribute per line in HTML, Vue and JSX.

    Valid Options:

    - ***false*** (default) Do not enforce single attribute per line.
    - ***true*** Enforce single attribute per line.

See the Prettier Options [doc page] for more details and examples.

### Project-level Settings

JsPrettier supports [project-level settings], specified in `<project_name>.sublime-project` files.

To override [previous configurations](#plugin-settings-and-prettier-options) with your project-level settings,
add a new `js_prettier` key and section under `settings` as shown in the [example below](#example-sublime-text-project-file).

#### Example Sublime Text Project File

```json
{
    "folders": [
        {
            "path": "."
        }
    ],
    "settings": {
        "js_prettier": {
            "debug": false,
            "prettier_cli_path": "",
            "node_path": "",
            "auto_format_on_save": false,
            "auto_format_on_save_excludes": [],
            "auto_format_on_save_requires_prettier_config": false,
            "allow_inline_formatting": false,
            "custom_file_extensions": [],
            "max_file_size_limit": -1,
            "disable_tab_width_auto_detection": false,
            "disable_prettier_cursor_offset": false,
            "additional_cli_args": {},
            "prettier_options": {
                "printWidth": 80,
                "tabWidth": 2,
                "singleQuote": false,
                "trailingComma": "all",
                "bracketSpacing": true,
                "bracketSameLine": false,
                "jsxSingleQuote": false,
                "semi": true,
                "requirePragma": false,
                "proseWrap": "preserve",
                "arrowParens": "always",
                "htmlWhitespaceSensitivity": "css",
                "quoteProps": "as-needed",
                "vueIndentScriptAndStyle": false,
                "embeddedLanguageFormatting": "auto",
                "editorconfig": true,
                "singleAttributePerLine": false
            }
        }
    }
}
```

### Prettier Configuration Files

When [Prettier configuration files] are detected, options defined in *Sublime
Text* are ignored, except for `parser`, `tabWidth`, and `useTabs`.
These options are automatically set based on syntax settings of the current file
or selection(s) defined in Sublime Text.

#### Custom Prettier Config File Path

To specify a custom Prettier config path, simply add a `--config <path>`
key-value item to `additional_cli_args`. Here's an example:

```json
{
    "additional_cli_args": {
        "--config": "~/some/path/from/my/home/.prettierrc",
        "--config-precedence": "prefer-file",
        "--ignore-path": "${project_path}/.prettierignore"
    }
}
```

#### Disable Prettier Config File Discovery

You can also add the `--no-config` option to the `additional_cli_args` setting,
and tell Prettier not to attempt to find config files.

```json
{
    "additional_cli_args": {
        "--no-config": ""
    }
}
```

#### Prettier Ignore Config File Discovery (`.prettierignore`)

When the [`--ignore-path`] option is NOT specified in `additional_cli_args`,
the plugin will search for a `.prettierignore` file in the same directory of
the source file, then the active Sublime Text project's root directory. If
neither path can be resolved, search up the directory tree, and finally look
in the user's home directory.

## Prettier Community Plugins

Here's an [example SublimeText project](https://github.com/jonlabelle/SublimeJsPrettier/files/6498394/jsprettier-and-prettier-community-plugin-example.zip)
from [#239](https://github.com/jonlabelle/SublimeJsPrettier/issues/239)
that uses the Prettier Community Plugin [prettier-plugin-go-template](https://github.com/NiklasPor/prettier-plugin-go-template)
to format `*.gohtml` files.

And another [example project](https://github.com/jonlabelle/SublimeJsPrettier/files/6527323/jsprettier-and-prettier-plugin-sort-imports.zip)
from [#240](https://github.com/jonlabelle/SublimeJsPrettier/issues/240) that
uses [prettier-plugin-sort-imports](https://github.com/trivago/prettier-plugin-sort-imports)
to sort imports.

## Issues

To report a bug or make a suggestion, please [open a new issue] selecting the
appropriate issue template: [Bug], [Feature], or [Question].

Be sure to follow the guidelines outlined in each template; otherwise, your
submission may be closed.

## Changes

Please visit the [Changelog] page for a complete list of changes.

## License

[MIT]

## Author

[Jon LaBelle](https://github.com/jonlabelle)

[Watch a Quick Demo]: https://github.com/jonlabelle/SublimeJsPrettier/blob/master/screenshots/demo.gif
[Prettier]: https://prettier.io
[Package Control]: https://packagecontrol.io/packages/JsPrettier
[Sublime Text]: https://www.sublimetext.com
[JsPrettier]: https://github.com/jonlabelle/SublimeJsPrettier
[Node.js]: https://nodejs.org
[project-level settings]: https://sublime-text-unofficial-documentation.readthedocs.io/en/latest/reference/projects.html
[tab_size]: https://sublime-text-unofficial-documentation.readthedocs.io/en/latest/reference/settings.html#whitespace-and-indentation
[***translate_tabs_to_spaces***]: https://sublime-text-unofficial-documentation.readthedocs.io/en/latest/reference/settings.html#whitespace-and-indentation
[yarn]: https://yarnpkg.com
[npm]: https://www.npmjs.com
[pnpm]: https://pnpm.io
[zip file]: https://github.com/jonlabelle/SublimeJsPrettier/archive/master.zip
[Sublime Text Packages directory]: #default-st-paths
[custom key binding]: https://sublime-text-unofficial-documentation.readthedocs.io/en/latest/customization/key_bindings.html
[Prettier Configuration files]: https://prettier.io/docs/en/configuration.html
[Changelog]: https://github.com/jonlabelle/SublimeJsPrettier/blob/master/CHANGELOG.md
[MIT]: https://github.com/jonlabelle/SublimeJsPrettier/blob/master/LICENSE
[doc page]: https://prettier.io/docs/en/options.html
[`--ignore-path`]: https://prettier.io/docs/en/cli.html#--ignore-path
[whitespace-sensitive formatting]: https://prettier.io/blog/2018/11/07/1.15.0.html#whitespace-sensitive-formatting
[`--log-level`]: https://prettier.io/docs/en/cli.html#--log-level
[open a new issue]: https://github.com/jonlabelle/SublimeJsPrettier/issues/
[Prettier v1.17+]: https://prettier.io/blog/2019/04/12/1.17.0.html
[\.editorconfig]: https://editorconfig.org/
[Bug]: https://github.com/jonlabelle/SublimeJsPrettier/issues/new?assignees=jonlabelle&labels=investigating&projects=&template=bug.yml&title=%5BBug%5D+
[Feature]: https://github.com/jonlabelle/SublimeJsPrettier/issues/new?assignees=jonlabelle&labels=enhancement&projects=&template=feature.yml&title=%5BEnhancement%5D+
[Question]: https://github.com/jonlabelle/SublimeJsPrettier/issues/new?assignees=&labels=question&projects=&template=question.yml&title=%5BQuestion%5D+
