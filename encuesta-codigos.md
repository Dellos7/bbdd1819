```java
class Calculadora {

    private double num = 0;

    public Calculadora( double num ) {
        this.num = num;
    }

    public double raizCuadrada() {
        return Math.sqrt(this.num);
    }

}

public static void main( String args[] ) {
    Calculadora calculadora = new Calculadora(5);
    double raizCuadrada = calculadora.raizCuadrada();
    System.out.println(raizCuadrada);
}
````

```java

public double raizCuadrada( double num ) {
    return Math.sqrt(num);
}

public static void main( String args[] ) {
    double raizCuadrada = raizCuadrada(5);
    System.out.println(raizCuadrada);
}
````

```java
String [] arr = { "Hola", "qué", "tal" };
String resultado = arr[arr.length - 1] + "amajal".substring(1);
```

```java
String a = "12345";
int b = 12345;
String resultado = ( a.equals( b.toString() ) ? "¯\_(ツ)_/¯" : "(⊙＿⊙’)" )
```

```java
Map<String, String> mapaCampeones = new HashMap<>();
mapaCampeones.put("Anivia", "Mid");
mapaCampeones.put("Lee Sin", "Jungla");
mapaCampeones.put("Vayne", "ADC");
mapaCampeones.put("Sona", "Support");

mapaCampeones.forEach( (clave, valor) -> {
    System.out.println( clave + "->" + valor );
});
```

```
Anivia->Mid
Lee Sin->Jungla
Vayne->ADC
Sona->Support
```

```
Mid->Anivia
Jungla->Lee Sin
ADC->Vayne
Support->Sona
```