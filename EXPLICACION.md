# Explicación del workflow seguro

## Permissions
- El workflow y los jobs usan permisos mínimos (`read` por defecto, `write` solo donde es estrictamente necesario).
- Ejemplo: Solo el job de despliegue a producción tiene permiso para `deployments`.

## Protections (Environments)
- Se usan entornos `staging` y `production`.
- `production` requiere aprobación manual de reviewers antes de desplegar.
- Esto previene despliegues accidentales o no autorizados.

## Evidencia de aprobación manual
- Toma una captura de pantalla del workflow esperando aprobación en la pestaña de Actions.
- Toma otra captura de la pantalla de aprobación en el entorno `production`.

## Instrucciones para capturas
1. **Secrets y variables:**
   - Captura la pantalla de la lista de secrets y variables en Settings → Secrets and variables → Actions.
2. **Environments:**
   - Captura la configuración de los entornos `staging` y `production`.
   - En `production`, muestra los reviewers requeridos y la protección manual.
3. **Aprobación manual:**
   - Cuando el workflow esté esperando aprobación para desplegar en producción, captura la pantalla.
4. **Explicación:**
   - Adjunta este archivo como parte de la entrega.

## Riesgos y buenas prácticas
- **No imprimir secretos:** Nunca uses `echo ${{ secrets.MI_SECRET }}` en los logs.
- **No usar @main en actions externas:** Usa versiones fijas (ejemplo: `actions/checkout@v4`).
- **Permisos mínimos:** No uses `permissions: write-all`.
- **Riesgos de exponer secretos:** Si un secret se imprime o se filtra, puede ser usado por atacantes para comprometer sistemas.
- **Riesgos de actions externas:** Actions de terceros pueden contener código malicioso. Usa solo actions confiables y versiones fijas.
- **Riesgos de permisos excesivos:** Permisos innecesarios pueden permitir a un atacante escalar privilegios si compromete el workflow.
