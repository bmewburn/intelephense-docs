# Intelephense

Intelephense is a PHP language server adhering to the [Language Server Protocol](https://microsoft.github.io/language-server-protocol/specification).

### Requirements
[Node.js 12+](https://nodejs.org)

### Installation
```
npm i intelephense -g
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
    //Optional absolute path to storage dir. Defaults to os.tmpdir().
    storagePath?: string;
    
    //Optional absolute path to a global storage dir. Defaults to os.homedir().
    globalStoragePath?: string;
    
    //Optional licence key or absolute path to a text file containing the licence key.
    //Licence key can be provided here if the client does not support workspace/configuration requests.
    licenceKey?: string;
    
    //Optional flag to clear server state.
    clearCache?: boolean;
}
```

### Capabilities
<details>
	<summary>Server capabilities JSON returned from `initialize` request.</summary>
	
```javascript
{
	textDocumentSync: TextDocumentSyncKind.Incremental,
	documentSymbolProvider: true,
	workspaceSymbolProvider: true,
	completionProvider: {
		triggerCharacters: [
			//php
			'$', '>', ':', '\\', '/',
			//phpdoc
			'*',
			// html/js
			'.', '<'
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
	documentFormattingProvider: true,	//Dynamic registration if available.
	documentHighlightProvider: true,	//Dynamic registration if available.
	workspace: {
		workspaceFolders: {
			supported: true,
			changeNotifications: true
		}
	},
	foldingRangeProvider: true,		//With licence key only. Dynamic registration if available.
	implementationProvider: true,		//With licence key only. Dynamic registration if available.	
	declarationProvider: true,		//With licence key only. Dynamic registration if available.
	renameProvider: { 			//With licence key only. Dynamic registration if available.
		prepareProvider: true 
	},
	typeDefinitionProvider: true		//With licence key only. Dynamic registration if available.
}
```
</details>

### Configuration Options
<details>
	<summary>JSON schema for `workspace/configuration` request data</summary>
	
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
    "intelephense.completion.triggerParameterHints": {
    	"type": "boolean",
        "default": true,
        "description": "Method and function completions will include parentheses and trigger parameter hints.",
        "scope": "window"
    },
    "intelephense.completion.maxItems": {
    	"type": "number",
        "default": 100,
        "description": "The maximum number of completion items returned per request.",
        "scope": "window"
    },
    "intelephense.format.enable": {
        "type": "boolean",
        "default": true,
        "description": "Enables formatting.",
        "scope": "window"
    },
    "intelephense.licenceKey": {
        "type": "string",
        "description": "Enter your intelephense licence key here to access premium features.",
        "scope": "application"
    },
    "intelephense.telemetry.enabled": {
    	"type": "boolean",
        "description": "Anonymous usage and crash data will be sent to Azure Application Insights.",
        "scope": "window",
        "default": null
    },
    "intelephense.rename.exclude": {
    	"type": "array",
        "items": {
        	"type": "string"
        },
        "default": [
        	"**/vendor/**"
        ],
        "description": "Glob patterns to exclude files and folders from having symbols renamed. Rename operation will fail if references and/or definitions are found in excluded files/folders.",
        "scope": "resource"
    },
    "intelephense.environment.documentRoot": {
    	"type": "string",
        "description": "The directory of the entry point to the application (index.php). Defaults to the first workspace folder. Used for resolving script inclusion.",
        "scope": "window"
    },
    "intelephense.environment.includePaths": {
    	"type": "array",
        "items": {
        	"type": "string"
        },
        "description": "The include paths (as individual path items) as defined in the include_path ini setting. Used for resolving script inclusion.",
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
</details>

### Licence
This is proprietary software. Please see licence in [LICENSE.txt](https://github.com/bmewburn/intelephense-docs/blob/master/LICENSE.txt).
