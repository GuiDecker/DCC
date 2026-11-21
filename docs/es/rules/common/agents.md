# Orquestación de Agentes

## Agentes Disponibles

Los agentes de ECC se distribuyen con el plugin `ecc@ecc`, no en `~/.claude/agents/`.
Se invocan a través de la herramienta Agent con un `subagent_type` con ámbito de plugin:

```text
Agent(subagent_type: "dcc:planner", prompt: "...")
```

| Agente | Propósito | Cuándo Usar |
|--------|-----------|-------------|
| dcc:planner | Planificación de implementación | Features complejas, refactoring |
| dcc:architect | Diseño de sistemas | Decisiones arquitectónicas |
| dcc:tdd-guide | Desarrollo guiado por pruebas | Nuevas features, corrección de bugs |
| dcc:code-reviewer | Revisión de código | Después de escribir código |
| dcc:security-reviewer | Análisis de seguridad | Antes de los commits |
| dcc:build-error-resolver | Corrección de errores de build | Cuando el build falla |
| dcc:e2e-runner | Testing E2E | Flujos de usuario críticos |
| dcc:refactor-cleaner | Limpieza de código muerto | Mantenimiento de código |
| dcc:doc-updater | Documentación | Actualización de docs |
| dcc:rust-reviewer | Revisión de código Rust | Proyectos Rust |
| dcc:harmonyos-app-resolver | Desarrollo de apps HarmonyOS | Proyectos HarmonyOS/ArkTS |

Para el roster completo de 68 agentes, ver `/ecc:ecc-guide`.

## Uso Inmediato de Agentes

Sin necesidad de prompt del usuario:
1. Solicitudes de features complejas - Usar el agente **dcc:planner**
2. Código recién escrito/modificado - Usar el agente **dcc:code-reviewer**
3. Corrección de bug o nueva feature - Usar el agente **dcc:tdd-guide**
4. Decisión arquitectónica - Usar el agente **dcc:architect**

## Ejecución Paralela de Tareas

SIEMPRE usar ejecución paralela de tareas para operaciones independientes:

```markdown
# CORRECTO: Ejecución paralela
Lanzar 3 agentes en paralelo:
1. Agente 1: Análisis de seguridad del módulo de auth
2. Agente 2: Revisión de rendimiento del sistema de caché
3. Agente 3: Verificación de tipos de las utilidades

# INCORRECTO: Secuencial cuando no es necesario
Primero agente 1, luego agente 2, luego agente 3
```

## Análisis Multi-Perspectiva

Para problemas complejos, usar sub-agentes con roles divididos:
- Revisor factual
- Ingeniero senior
- Experto en seguridad
- Revisor de consistencia
- Verificador de redundancias
