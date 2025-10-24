Unha cuestión fundamental no deseño dun CPD é a colocación dos servidores en función da xestión do fluxo de aire e da tolerancia a eventuais fallos eléctricos.

**Xeralmente, os servidores enrackables colócanse na parte inferior do rack, debaixo do patch panel, por razóns de eficiencia na refrixeración.**
## O máis importante: xestión do fluxo de aire

A maioría dos servidores de rack están deseñados para un **fluxo de aire de diante cara a atrás**:
*   **Frontal (cara ó pasillo frío):** absorbe aire frío.
*   **Traseira (cara ó pasillo quente):** expulsa aire quente.

Para que este sistema sexa eficiente, debemos crear un "pasillo frío" e un "pasillo quente". A colocación dos equipos no rack debe facilitar que o aire frío flúa sen mesturarse co quente de forma prematura.

### Escenario Práctico: patch panel arriba

Neste caso contamos con 2 racks:
- Rack para servidores
- Rack para switches de rede

O noso patch panel está na parte superior do rack de switches contiguo, pero en xeral a distribución ideal sería:

1.  **Parte superior do rack:** **patch panels e cableado.**
    *   Os patch panels son equipamento pasivo (non xeran calor).
    *   Colocalos arriba evita que interrompan o fluxo de aire frío que debe chegar ás entradas dos servidores.
    *   Ademais, facilita a xestión do cableado, xa que os cables de rede poden sair directamente cara ó cableado horizontal do teito ou ás bandexas superiores.

2.  **Parte media do rack:** **switches de rede.**
    *   Os switches xeran unha cantidade significativa de calor. Colocalos no medio permite que o aire frío que sube desde abaixo lles chegue, e o seu aire quente expúlsase directamente ao pasillo quente sen afectar a outros equipos sensibles.

3.  **Parte inferior do rack:** **servidores.**
    *   Esta é a localización óptima. Os servidores absorben o aire máis frío e limpo directamente desde o pasillo frío.
    *   Se os servidores estivesen arriba, o aire que chegaría a eles xa estaría pre-quentado polo equipo de abaixo (switches, outros servidores), reducindo drasticamente a súa eficiencia de arrefriamento e podendo causar sobrequecemento.

4.  **Parte máis inferior (se hai):** **Sistemas de Alimentación Ininterrompida (SAI/UPS).**
    *   Os SAIs son xeralmente os equipos máis pesados e colocalos abaixo dá estabilidade ó rack. Ademais, o seu patrón de fluxo de aire pode ser diferente (ás veces de abaixo arriba) e evita interferir co dos servidores.

### Esquema da distribución típica dos elementos nun rack:

```
+-----------------------------------+   ˇ ˇ ˇ ˇ ˇ ˇ ˇ ˇ ˇ ˇ ˇ ˇ ˇ ˇ ˇ ˇ
|        PATCH PANELS               |   -- Cables de Rede cara ó teito --
+-----------------------------------+
|         SWITCHES                  |   <-- Xera calor (aire quente atrás)
+-----------------------------------+
|                                   |
|         SERVERS                   |   <-- Absorbe aire frío do pasillo frío
|         SERVERS                   |
|         SERVERS                   |
+-----------------------------------+
|          SAI/UPS                  |   (Equipo pesado, fluxo de aire variable)
+-----------------------------------+
```
*Pasillo Frío (diante do rack) --> Pasillo Quente (detrás do rack)*

> Coloca-los **servidores na parte inferior do rack**, incluso cando o patch panel está na parte superior. Isto optimiza a refrixeración, que é un dos factores máis críticos para a lonxevidade e rendemento do hardware nun CPD.
