# [EC2](https://aws.amazon.com/es/ec2/)

(Virtual machine servers in the Cloud)

## Tipos de EC2

* On Demand
  * Pagas un precio fijo por hora (o segundo). Windows -> hora | Linux -> segundo
  * Flexible y barato
* Reserved
  * Contratas entre 1 y 3 años. Tienes descuentos por tiempo de uso
* On Spot
  * Apuestas el precio que quieres pagar (por hora o segundo)
  * Si el precio de *Spot* es mayor que el que has apostado -> no pasa nada
  * Si el precio de *Spot* es menor que el que has apostado -> puedes lanzar tus máquinas.
    * Si el precio del *Spot* vuelve a subir una hayas lanzado tus máquinas, éstas se detendrán.
  * Billing:
    * Si terminas la instancia a mitad de la hora pagada -> **te cobran** la hora entera
    * Si AWS te termina la instancia (por la subida de precio) a mitad de la hora entera -> **gratis**
* Dedicaded Hosts
  * Servidor físico dedicado exclusivamente para ti

## [Tipos de Instancias EC2](https://aws.amazon.com/es/ec2/instance-types/)

### Familias
>X0 -> X: Letra que indica la finalidad | 0: Número que indica la versión

* **D**2 -> **Density** (*Capacidad*)
* **R**4 -> **Memory/RAM** (*Memoria*)
* **M**4 -> **Main general purpose** (*Genéricas*)
* **C**4 -> **Compute** (*CPU*)
* **G**2 -> **Graphics** (*Memoria gráfica*)
* **I**2 -> **High Speed Storage** (*Memoria rápida*)
* **F**1 -> **Hardware Acceleration** (*IOPS*)
* **T**2 -> **Lowest cost, General purpose** (*Más comunes*)
* **P**2 -> **General purpose with graphics**
* **X**1 -> **Extreme Memory**


## EBS

* Store volumes
  * Discos que se acoplan a EC2 para que éstos tengan almacenamiento
* Aun que se creen en una Zona concreta, se auto replican para protegerse de fallos

### Tipos EBS
* GP2
  * **SSD** General Purpose -> ~ 10000 IOPS
* IO1
  * **SSD** I/O Intensive applications (like Databases) -> + 10000 IOPS (~ 20000 IOPS)
* ST1
  * **HDD** Big Data, Data warehouse
* SC1
  * Cold **HDD** File server. Acceso de datos **poco** frecuente
* Standart
  * **HDD Bootable** Barato, acceso de datos **muy** poco frecuente

> Los HDD no se pueden utilizar como disco de arranque (Boot volume) para las EC2. Solo el **Standart**

## Importante
* No se pueden montar 1 EBS para varios EC2
  * Para ello habrá que usar **EFS** (Elastic File System) -> Permite intercambiar archivos entre volúmenes

---

[<small>⬅ Atrás</small>](./index.md)