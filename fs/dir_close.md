<!-- YAML
added: v12.12.0
-->

* 返回: {Promise}

异步地关闭目录的底层资源句柄。 
随后的读取将会导致错误。

返回一个	`Promise`，将会在关闭资源之后被resolve。

