# Crear rutas y maneja r peticiones 

``` go
package routes

import (
	"net/http"

	"github.com/gin-gonic/gin"
)

func SetupRoutes(r *gin.Engine) {

	r.GET("/", func(c *gin.Context) {
		c.String(200, "¡Hola, Mundo!\n")
		//c.JSON(200, gin.H{"mensaje": "¡Hola, Mundo! desde Gin"})
	})
	r.GET("/saludo/:nombre", func(c *gin.Context) {
		nombre := c.Param("nombre")
		c.String(http.StatusOK, "¡Hola, %s ! \n", nombre)

	})

}
package main

import (
	"Gin/routes"

	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()
	routes.SetupRoutes(r)
	r.Run(":8080")

}


```