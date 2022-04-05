# Macowins

## Pseudocodigo

```wollok
object macowins {
    var ventas

    method gananciasDelDia(fecha){
        var ventasDelDia = ventas.filter { unaVenta => unaVenta.fecha() == fecha }
        return ventasDelDia.sum {unaVenta => unaVenta.precioFinal()}
    }
}
```

### Prendas

```wollok
class Prenda {

    var precio
    var estadoPrenda

    method calcularPrecio(){
        return estadoPrenda.calculate(precio)
    }

}
```

```wollok
interface estado {
     method calculate(precioBase)
}

object nueva implements estado {

    method calculate(precioBase){
        return precioBase
    }

}

class Promocion implements estado {

    var valorFijo

    method calculate(precioBase){
        return precioBase - valorFijo
    }

}

object liquidacion implements estado {

    method calculate(precioBase){
        return precioBase / 2
    }

}
```

### Ventas

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

```wollok
interface formaDePago {
     method precioFinal(subtotal)
}

object efectivo implements formaDePago {
     method precioFinal(subtotal) {
          return subtotal
     }
}

class Tarjeta implements formaDePago {
     var cantidadCuotas
     var coeficiente

     method precioFinal(subtotal) {
          var recargo = cantidadCuotas * coeficiente + subtotal * 0.01
          return subtotal + recargo
     }
}
```
