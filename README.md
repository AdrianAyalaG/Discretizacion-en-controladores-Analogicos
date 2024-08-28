15/08/2024
# Discretizacion en controladores Analogicos
Se trata de expresar una señal analoga en continua teniendo un balance entre el espacio de LaPalce y la transformada Z, y para ello existen varios metodos.

## 1. Método de invarianza al impulso
El método de invarianza al impulso consiste un sistema discreto que al aplicarle un impulso su salida sea idéntica a la funcion de transferencia del sistema en los instantes de muestreo.
* Se tiene una funcion estrictamente propia en tiempo continuo C(s) y un tiempo de muestreo T muy pequeño:

  $$C(z)=TZ[L^{-1}[C(s)]_{t=KT}]$$

 💡 Ejemplo:    $$C(s)=\frac{5(s+2)}{(s+1)(s+10)}$$ 

 * Aplicando fracciones parciales:

  $$C(s)=\frac{5/9}{(s+1)}+\frac{40/9}{(s+10)}$$
  
 * Usando la transformada inversa de LaPlace se obtine:

   $$L^{-1}(C(s))=\frac{5}{9}*e^{-t}+\frac{40}{9}*e^{-10t}$$
  
 * Discretizando la expresion:

   $$L^{-1}(C(s))_{t=kT}=\frac{5}{9e^{-kT}}+\frac{40}{9e^{-10kT}}$$
  
 * Por lo tanto:

    $$C(z)=TZ(\frac{5}{9}e^{-kT}+\frac{40}{9}e^{-10kT})$$

 * De las tablas de la transformada Z se obtiene:

     $$C(z)=T(\frac{5z}{9(z-e^{-T})}+\frac{40z}{9(z-e^{-10T})})$$

## 2.Método de invarianza al paso
Para este metodo se igualan las transformadas inversas tanto de LaPlace y la transformada Z:

$$Z^{-1}[C(z)\frac{z}{z-1}]=L^{-1}[C(s)\frac{1}{s}]$$

Al despejar la transformada Z:

$$C(z)=\frac{z-1}{z}Z[L^{-1}(C(s)\frac{1}{s})]$$

💡 Ejemplo:    

$$C(s)=\frac{2(s-2)}{(s+1)(s+3)}$$ 

* Se divide por s para obtener la respuesta al escalon:

$$\frac{C(s)}{s}=\frac{2(s-2)}{s(s+1)(s+3)}$$ 

* Se aplican fracciones parciales:

$$C(s)=\frac{-4/3}{s}-\frac{3}{s+1}-\frac{5/3}{s+3}$$ 

* La respuesta al paso en el tiempo es:

$$L^{-1}[\frac{C(s)}{s}]=-\frac{4}{3}-3e^{-t}-\frac{5}{3}e^{-3t}$$

* Por tablas de la transformada Z:

$$Z(L^{-1}[\frac{C(s)}{s}])=-\frac{4z}{3(z-1)}-\frac{3z}{z-e^{-T}}-\frac{5z}{3(z-e^{-3T})}$$

* De la definicion:

$$C(z)=\frac{z-1}{z}(-\frac{4z}{3(z-1)}-\frac{3z}{z-e^{-T}}-\frac{5z}{3(z-e^{-3T})})$$

* Resolviendo :
  $$C(z)=\frac{0.116z-0.523}{z^{2}-0.803z+0.135}$$

## 3. Método Euler Adelante
* La derivada en tiempo discreto se puede expresar de la siguiente manera:

$$\frac{d}{dkT}x(kT)=\frac{x(k+1)-x(k)}{T}$$

* Se sabe que:

$$L[\frac{d}{dt}x(t)]=X(s)$$

* Al aplicar la transformada Z:

$$Z[\frac{x(k+1)-x(k)}{T}]=\frac{z-1}{T}X(z)$$

* Se obtiene:

$$sX(s)=\frac{z-1}{T}X(z)$$

$$s=\frac{z-1}{T}$$

* En este metodo un controlador estable en tiempo continuo no siempre es estable en tiempo discreto.

## 4. Método Euler Atras
* La derivada en tiempo discreto se puede expresar de la siguiente manera:

$$\frac{d}{dkT}x(kT)=\frac{x(k)-x(k-1)}{T}$$

* Se sabe que:

$$L[\frac{d}{dt}x(t)]=X(s)$$

* Al aplicar la transformada Z:

$$Z[\frac{x(k)-x(k-1)}{T}]=\frac{1-z^{-1}}{T}X(z)$$

* Se obtiene:

$$sX(s)=\frac{1-z^{-1}}{T}X(z)$$

$$s=\frac{1-z^{-1}}{T} = \frac{z-1}{Tz}$$

* En este metodo un controlador estable en tiempo continuo es estable en tiempo discreto.

## 5. Método trapezoidal o "Tustin"
* La equivalencia es:

$$s=\frac{2(z-1)}{T(z+1)}$$

* O tambien:

$$z=\frac{1+\frac{Ts}{2}}{1-\frac{Ts}{2}}$$

## EJERCICIOS
### Invarianza al paso
$$H(s)=\frac{10(s+1)}{(s+3)(s+7)}$$ 

* Se divide por s para obtener la respuesta al escalon:

$$\frac{H(s)}{s}=\frac{10(s+1)}{s(s+3)(s+7)}$$ 

* Se aplican fracciones parciales:

$$H(s)=\frac{10}{21s}-\frac{5}{3(s+3)}-\frac{15}{7(s+7)}$$ 

* La respuesta al paso en el tiempo es:

$$L^{-1}[\frac{H(s)}{s}]=\frac{10}{21}-\frac{5}{3}e^{-3t}-\frac{15}{7}e^{-7t}$$

* Por tablas de la transformada Z:

$$Z(L^{-1}[\frac{H(s)}{s}])=\frac{10z}{21(z-1)}-\frac{5z}{3(z-e^{-3T})}-\frac{15z}{7(z-e^{-7T})}$$

* De la definicion:

$$C(z)=\frac{z-1}{z}(\frac{10z}{21(z-1)}-\frac{5z}{3(z-e^{-3T})}-\frac{15z}{7(z-e^{-7T})})$$

### Método de Euler Adelante

$$D(s)=\frac{2s+4}{s^{2}+4s+8}$$

* Se sabe que:

$$s=\frac{z-1}{T}$$

* Se sustituye s en H(s) para tener H(z):

$$D(z)=\frac{2\frac{z-1}{T}+4}{(\frac{z-1}{T})^{2}+4\frac{z-1}{T}+8}$$

* Tomando T=1:

$$D(z)=\frac{2(z-1)+4}{(z-1)^{2}+4(z-1)+8}=\frac{2z-2+4}{z^{2}-2z+1+4z-4+8}$$

* D(z) seria:

$$D(z)=\frac{2z+2}{z^{2}+2z+5}$$

## Conclusion 
La elección del método de discretización depende de las características del sistema y de los requisitos específicos del control. Para aplicaciones donde la estabilidad es crítica, el método de Euler Atrás o el método Tustin son preferibles. Si la respuesta a un impulso o escalón es prioritaria, los métodos de invarianza al impulso o al paso son más adecuados.
## Referencias
[1]“AulasVirtualesECCI: Entrar al sitio”, Edu.co. [En línea]. Disponible: https://aulas.ecci.edu.co/course/view.php?id=9304 . [Consulta: 20 de agosto de 2024].
