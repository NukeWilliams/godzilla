# godzilla

[![forthebadge](https://forthebadge.com/images/badges/made-with-go.svg)](https://forthebadge.com)

- A powerful go web framework for highly scalable and resource efficient web application

## Installation:
```
go get -u github.com/godzillaframework/godzilla
```

## Features:
- Fast
- Lightweight
- Secure
- Easy Peasy :)

## Examples:

- a simple api

```golang
package main

import "github.com/godzillaframework/godzilla"

func main() {
	gz := godzilla.New()

	gz.Get("/index", func(ctx godzilla.Context) {
		ctx.SendString("Hello EveryOne!!!")
	})

	gz.Start(":9090")
}
```

- params
```golang
package main

import "github.com/godzillaframework/godzilla"

func main() {
    gz := godzilla.New()

    gz.Get("/users/:user", func(ctx godzilla.Context) {
        ctx.SendString(ctx.Param("user"))
    })

    gz.Start(":8080")
}
```

- static files
```golang
package main

import "github.com/godzillaframework/godzilla"

func main() {
    gz := godzilla.New()

    gz.Static("/imgs", "./images")

    /* go to localhost:8080/imgs/image.png */

    gz.Start(":8080")
}
```

- middleware
```golang
package main

import (
	"log"

	"github.com/godzillaframework/godzilla"
)

func main() {

	gz := godzilla.New()

	logMiddleware := func(ctx godzilla.Context) {
		log.Printf("log message!")

		ctx.Next()
	}

	unAuthorizedMiddleware := func(ctx godzilla.Context) {
		ctx.Status(godzilla.StatusUnauthorized).SendString("You are unauthorized to access this page!")
	}

	gz.Use(logMiddleware)

	gz.Get("/hello", func(ctx godzilla.Context) {
		ctx.SendString("Hello World!")
	})

	gz.Get("/protected", unAuthorizedMiddleware, func(ctx godzilla.Context) {
		ctx.SendString("You accessed a protected page")
	})

	gz.Static("/main", "./index.html")

	gz.Start(":8080")
}

```

- for more tutorials visit the [docs](https://github.com/godzillaframework/godzilla/blob/master/docs/learngodzilla.md)