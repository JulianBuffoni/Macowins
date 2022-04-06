# Diseño de Sistemas 2022 - Macowins
## Integrantes
| Alumno                        | Legajo  |
| ----------------------------- | ------- |
| Bruno Juan Pablo              | 1768920 |
| Buffoni Julian                | 1756760 |
| Fusse Fausto                  | 1757519 |
| Gette Delfina                 | 1722712 |
| Riquelme Blaffet Pablo Daniel | 1632784 |


## Pseudocodigo
### Prendas
```wollok
class Prenda {
    var nombre
    var tipo
    var precioBase
    var estadoPrenda

    method calcularPrecio(){
        return estadoPrenda.calcularPrecio(precioBase)
    }

}
```
#### Estados de Prenda
```wollok

object nueva {

    method calcularPrecio(precioBase){
        return precioBase
    }

}

class Promocion {

    var valorFijo

    method calcularPrecio(precioBase){
        return precioBase - valorFijo
    }

}

object liquidacion {

    method calcularPrecio(precioBase){
        return precioBase / 2
    }

}
```

### Ventas
```wollok
object macowins {
    var ventas

    method gananciasDelDia(fecha){
        var ventasDelDia = ventas.filter { unaVenta => unaVenta.fecha() == fecha }
        return ventasDelDia.sum {unaVenta => unaVenta.precioFinal()}
    }

    method precioPrenda(prenda){
        return prenda.calcularPrecio()
    }
}
```

```wollok
class Venta {
     var prendas
     var fecha
     var formaDePago

     method calcularSubtotal() {
          return prendas.sum {unaPrenda => unaPrenda.calcularPrecio()}
     }

     method precioFinal() {
          return formaDePago.precioFinal(this.calcularSubtotal())
     }
}
```
#### Formas de Pago
```wollok

object efectivo {
     method precioFinal(subtotal) {
          return subtotal
     }
}

class Tarjeta {
     var cantidadCuotas
     var coeficiente

     method precioFinal(subtotal) {
          var recargo = cantidadCuotas * coeficiente + subtotal * 0.01
          return subtotal + recargo
     }
}
```