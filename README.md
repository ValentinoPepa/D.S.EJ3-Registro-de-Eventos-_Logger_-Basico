# D.S.EJ3-Registro-de-Eventos-_Logger_-Basico

[Logger.java](https://github.com/user-attachments/files/32867643/Logger.java)

<img width="803" height="398" alt="image" src="https://github.com/user-attachments/assets/013a525b-b628-4321-b095-56029ec96f01" />

FUNCIONAMIENTO

- **Acceso único centralizado:** Ningún componente invoca _new Logger()_. EN su lugar, cuando clases de distintos modulos (Autenticacion, Servicios, BD) necesitan registrar un suceso, solicitan la rederencia mediante _Logger.getInstance()_.
- **Construcción de entradas enriquecidas:** Al invocar cualquiera de los métodos de registro (_info_, _warning_, _error_), la clase obtiene de forma automática la hora exacta del sistema (_LocalDataTime_), le antepone el tipo de severidad y formatea la cadena antes de imprimirla
- **Garantía de salida ordenada:** Gracias a la sincronización en el canal de salida, las solicitudes concurrentes se procesa en la cola secuencial, evitando que los mensajes se solapen o corrompen la traza

LOGICA

- **Encapsulamiento del ciclo de vida:** Al privatizar el constructor, el patron Singleton le otroga a la clase el control total de su propia creacion.
- **Canalizador único de E/S:** Cuando múltiples componentes intentan escribir sobre el mismo archivo o flujo de consola, crear múltiples objetos generaría contención o bloqueos. Canalizar todas la llamadas a través de un único objeto coordinado garantiza la integridad de los datos volcados
- **Identidad compartida en memoria:** Al evaluar _loggerAuth == loggerServicios_, la respuesta es _true_, confirmando que todos los componentes operan sobre una única fuente de verdad sin duplicar instancias.
