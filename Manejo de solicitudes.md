# Manejo se solicitudes Http

´´´
package routes

import (
	"net/http"

	"github.com/gin-gonic/gin"
)

// Usuario struct para representar la información del usuario
type Usuario struct {
	Nombre string `json:"nombre"`
	Email  string `json:"email"`
}

var usuarios []Usuario

func SetupRoutes(r *gin.Engine) {

	r.GET("/", func(c *gin.Context) {
		c.String(200, "¡Hola, Mundo!\n")
		//c.JSON(200, gin.H{"mensaje": "¡Hola, Mundo! desde Gin"})
	})
	r.GET("/saludo/:nombre", func(c *gin.Context) {
		nombre := c.Param("nombre")
		c.String(http.StatusOK, "¡Hola, %s ! \n", nombre)

	})

	r.POST("/usuarios/", func(c *gin.Context) {
		var nuevoUsuario Usuario
		if err := c.BindJSON(&nuevoUsuario); err != nil {
			c.JSON(http.StatusBadRequest, gin.H{
				"Error": "Error al decodificar el JSON",
			})
			return
		}
		if nuevoUsuario.Nombre == "" || nuevoUsuario.Email == "" {
			c.JSON(http.StatusBadRequest, gin.H{
				"Error": "Nombre y Email son campos requeridos",
			})
			return
		}

		usuarios = append(usuarios, nuevoUsuario)

		c.JSON(http.StatusOK, gin.H{
			"mensaje": "Usuario registrado", "datos": usuarios,
		})

	})

}


//go install github.com/gin-gonic/gin@latest

/*
Tambien se podría hacer utilizando el paquete Gin  y seguir las intrucciones: De hecho hay que hacerlo después de install

	go get -u github.com/gin-gonic/gin

Después de esto en go.mod y en go.sum se encuentran ya instaladas todas las dependencias
*/
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



´´´