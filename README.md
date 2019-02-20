# Intelephense

### [Support on Patreon](https://www.patreon.com/bmewburn)

Intelephense is a PHP language server adhering to the [Language Server Protocol](https://microsoft.github.io/language-server-protocol/specification).

### Installation
```
npm i intelephense -g
```

### Capabilities

```javascript
{
	textDocumentSync: TextDocumentSyncKind.Incremental,
	documentSymbolProvider: true,
	workspaceSymbolProvider: true,
	completionProvider: {
		triggerCharacters: [
			//php
			'$', '>', ':', '\\',
			//registered to enable request forwarding to html/js/css language servers
			'.', '<', '/'
		],
		resolveProvider: true
	},
	signatureHelpProvider: {
		triggerCharacters: ['(', ',']
	},
	definitionProvider: true,
	documentRangeFormattingProvider: true,
	referencesProvider: true,
	hoverProvider: true,
	documentHighlightProvider: true
}
```

### Run
```
intelephense {transport}
```  
Where `{transport}` is one of: 
* `--node-ipc`
* `--stdio`
* `--socket={number}`
* `--pipe={string}`

### Initialisation Options

```typescript
interface InitialisationOptions {
    //Optional absolute path to storage dir. Defaults to os.tmpdir()
    storagePath?: string;
    //Optional flag to clear server state
    clearCache?: boolean;
}
```

### Configuration Options

```json
{
    "intelephense.files.maxSize": {
        "type": "number",
        "default": 1000000,
        "description": "Maximum file size in bytes.",
        "scope": "window"
    },
    "intelephense.files.associations": {
        "type": "array",
        "default": [
            "*.php",
            "*.phtml"
        ],
        "description": "Configure glob patterns to make files available for language server features.",
        "scope": "window"
    },
    "intelephense.files.exclude": {
        "type": "array",
        "default": [],
        "description": "Configure glob patterns to exclude certain files and folders from all language server features.",
        "scope": "window"
    },
    "intelephense.stubs": {
        "type": "array",
        "default": [
            "apache",
            "bcmath",
            "bz2",
            "calendar",
            "com_dotnet",
            "Core",
            "csprng",
            "ctype",
            "curl",
            "date",
            "dba",
            "dom",
            "enchant",
            "exif",
            "fileinfo",
            "filter",
            "fpm",
            "ftp",
            "gd",
            "hash",
            "iconv",
            "imap",
            "interbase",
            "intl",
            "json",
            "ldap",
            "libxml",
            "mbstring",
            "mcrypt",
            "mssql",
            "mysql",
            "mysqli",
            "oci8",
            "odcb",
            "openssl",
            "password",
            "pcntl",
            "pcre",
            "PDO",
            "pdo_ibm",
            "pdo_mysql",
            "pdo_pgsql",
            "pdo_sqlite",
            "pgsql",
            "Phar",
            "posix",
            "pspell",
            "readline",
            "recode",
            "Reflection",
            "regex",
            "session",
            "shmop",
            "SimpleXML",
            "snmp",
            "soap",
            "sockets",
            "sodium",
            "SPL",
            "sqlite3",
            "standard",
            "superglobals",
            "sybase",
            "sysvmsg",
            "sysvsem",
            "sysvshm",
            "tidy",
            "tokenizer",
            "wddx",
            "xml",
            "xmlreader",
            "xmlrpc",
            "xmlwriter",
            "Zend OPcache",
            "zip",
            "zlib"
        ],
        "description": "Configure stub files for built symbols and common extensions. The default includes PHP core and all bundled extensions.",
        "scope": "window"
    },
    "intelephense.completion.insertUseDeclaration": {
        "type": "boolean",
        "default": true,
        "description": "Use declarations will be automatically inserted for namespaced classes, traits interfaces, functions, and constants.",
        "scope": "window"
    },
    "intelephense.completion.fullyQualifyGlobalConstantsAndFunctions": {
        "type": "boolean",
        "default": false,
        "description": "Global namespace constants and functions will be fully qualified (prefixed with a backslash).",
        "scope": "window"
    },
    "intelephense.format.enable": {
        "type": "boolean",
        "default": true,
        "description": "Enables formatting",
        "scope": "window"
    },
    "intelephense.trace.server": {
        "type": "string",
        "enum": [
            "off",
            "messages",
            "verbose"
        ],
        "default": "off",
        "description": "Traces the communication between client and server.",
        "scope": "window"
    }
}
```

### Licence
This is proprietary software. Please see licence in [LICENSE.txt](https://github.com/bmewburn/intelephense-docs/blob/master/LICENSE.txt).
