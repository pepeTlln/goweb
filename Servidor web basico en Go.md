# Servidor web básico en Go

```go
package main

import "github.com/gin-gonic/gin"

func main() {
	r := gin.Default()
	r.GET("/", func(c *gin.Context) {
		c.String(200, "¡Hola, Mundo!\n")
		c.JSON(200, gin.H{"mensaje": "¡Hola, Mundo! desde Gin"})
	})
	r.Run(":8080")

}

```
