# opexia-core-meta

Meta repositorio para coordinar los distintos stacks de OPEXIA (gateway CORE, plantillas EDGE y nodos físicos). Aquí sólo vive la documentación común y los enlaces a cada repositorio especializado; el código de cada stack se mantiene en su propia carpeta/repositorio para facilitar despliegues independientes.

## Estructura actual

```
opexia-core-meta/
├─ README.md                  # Este archivo: mapa de repos y guías generales
├─ ca-mosquitto.crt           # CA compartida para pruebas y staging
├─ opexia-core-certs/         # Copias locales de certificados/CA (no se versionan)
└─ opexia-core-gateway/       # Repo git del gateway maestro (docker-compose, NX-CORE-OPS)
```

## Repositorios componente

| Carpeta                | Repo recomendado                                     | Descripción breve                              |
|-----------------------|-------------------------------------------------------|------------------------------------------------|
| `opexia-core-gateway` | `git@github-opex:VictorOPEX/opexia-core-gateway.git`  | Stack Docker CORE (Mosquitto, Node-RED, Influx, Grafana) |
| *(pendiente)*         | `opexia-edge-template`                                | Plantillas y scripts para gateways EDGE        |
| *(pendiente)*         | `opexia-node-<tipo>`                                  | Firmware/config de nodos físicos (ej. count)   |

> Tip: cuando crees un nuevo stack, clónalo dentro de esta carpeta o usa `git submodule add` si quieres que este meta repo registre la referencia exacta.

## Flujo de trabajo sugerido

1. **Clonar meta repo** (opcional): `git clone git@github-opex:VictorOPEX/opexia-core-meta.git`.
2. **Clonar cada componente** dentro de esta carpeta:
   ```bash
   git clone git@github-opex:VictorOPEX/opexia-core-gateway.git
   git clone git@github-opex:VictorOPEX/opexia-edge-template.git        # cuando exista
   git clone git@github-opex:VictorOPEX/opexia-node-count.git           # ejemplo
   ```
3. **Trabajar por stack:** entra al repo correspondiente, modifica, commitea y haz `git push` al remoto propio.
4. **Actualizar meta:** si agregas/quitas componentes, documenta el cambio aquí y, si usas submódulos, actualiza los punteros con `git submodule update --remote`.

## Próximos pasos

1. Crear los repos `opexia-core-meta`, `opexia-gateway-core`, `opexia-edge-template`, etc. en GitHub/Azure y apuntar cada carpeta a su remoto.
2. Definir la convención de nombres para nodos (ej. `ND-COUNT-ZN1-057`) y reflejarla en los repos correspondientes.
3. Añadir a este README un inventario de gateways/nodos desplegados y qué commit/tag corre cada uno.
4. Automatizar certificados compartidos y scripts comunes (por ejemplo, un `scripts/` a nivel meta con tooling que usen todos los stacks).
