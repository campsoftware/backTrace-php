# backTrace-php

### Summary

Creates a BackTrace in PHP and returns a string.

### Calling Example

```php
phpBackTrace();
```
### Result

```
#0 xan\phpBackTrace() called at [ /etc/nginx/sites/app.foo.com/xanApp/xan/functions-internet.php:159 ]
#1 xan\sendEmailBackTrace() called at [ /etc/nginx/sites/app.foo.com/xanApp/app/UsersMT.php:144 ]
#2 xan\UsersMT->recMassage() called at [ /etc/nginx/sites/app.foo.com/xanApp/doSave.php:121 ]
#3 require_once() called at [ /etc/nginx/sites/app.foo.com/xanApp/router.php:34 ]
#4 require_once() called at [ /etc/nginx/sites/app.foo.com/xanApp/index.php:4 ]
```

### Function

```php
function phpBackTrace(): string {
	$backtrace = debug_backtrace( DEBUG_BACKTRACE_IGNORE_ARGS );
	$backtraceLog = '';
	
	// Process or format the backtrace array as needed
	foreach ( $backtrace as $index => $trace ) {
		// Namespace
		$namespace = isset( $trace[ 'class' ] ) ? $trace[ 'class' ] : '';
		
		// Class and type (-> for instance method, :: for static method)
		$class = isset( $trace[ 'class' ] ) ? $trace[ 'class' ] : '';
		$type = isset( $trace[ 'type' ] ) ? $trace[ 'type' ] : '';
		
		// Function name
		$function = isset( $trace[ 'function' ] ) ? $trace[ 'function' ] . "()" : "{main}";
		
		// File and line information
		$file = isset( $trace[ 'file' ] ) ? $trace[ 'file' ] : "unknown file";
		$line = isset( $trace[ 'line' ] ) ? $trace[ 'line' ] : "unknown line";
		
		// Construct backtrace log entry
		$backtraceLog .= "#" . $index . " " . ( $namespace ? $namespace . $type : '' ) . $function . " called at [ " . $file . ":" . $line . " ]\n";
	}
	
	// Return
	return $backtraceLog;
}
```
