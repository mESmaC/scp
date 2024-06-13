# Scope Language Support

This extension provides syntax highlighting and basic language support for the Scope programming language.

## Features

- Syntax highlighting for keywords, comments, strings, and variables.
- Support for modern Pascal-like syntax with additional features such as `mut`, `owner`, and `borrow` annotations.
- Curly brackets for block delimiters instead of `begin` and `end`.

## Example

```scope
program main;

uses
    crt,
    fphttpclient, // For HTTP requests
    regexpr;      // For regular expressions

var
    mut url: string;
    mut pageContent: string;
    mut re: TRegExpr;
    mut matches: array of string;

proc fetchPage(url: string) -> string {
    return TFPHTTPClient.SimpleGet(url);
};

proc extractLinks(content: string) -> array of string {
    re := TRegExpr.Create('<a href="([^"]+)"');
    try {
        if re.Exec(content) then {
            repeat
                matches.append(re.Match[1]);
            until not re.ExecNext;
        end;
    finally
        re.Free;
    end;
    return matches;
};

proc mainProcedure() {
    url := 'http://example.com';
    pageContent := fetchPage(url);
    matches := extractLinks(pageContent);
    
    for link in matches {
        writeln(link);
    }
};

init {
    mainProcedure();
};
```

##Requirements

There are no special requirements or dependencies for this extension.

##Extension Settings

This extension does not add any VS Code settings through the contributes.configuration extension point.

##Known Issues

There are no known issues at this time. Please report any issues you encounter on the GitHub repository.

##Release Notes

1.0.0

- Initial release of Scope language support.

##Working with Markdown

You can author your README using Visual Studio Code. Here are some useful editor keyboard shortcuts:

- Split the editor (Cmd+\ on macOS or Ctrl+\ on Windows and Linux).
- Toggle preview (Shift+Cmd+V on macOS or Shift+Ctrl+V on Windows and Linux).
- Press Ctrl+Space (Windows, Linux, macOS) to see a list of Markdown snippets.

For more information

- Visual Studio Code's Markdown Support: http://code.visualstudio.com/docs/languages/markdown
- Markdown Syntax Reference: https://help.github.com/articles/markdown-basics/

Enjoy!