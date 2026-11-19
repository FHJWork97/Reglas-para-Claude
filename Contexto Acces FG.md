# Contexto y estructura
Base de datos en Microsoft Access centrada en la gestión de pedidos/medicamentos fuera de guía, con un formulario principal (PedidosPlanta) y subformularios (FormularioDatos, FormularioRegistro y HistoricoControl con HistoricoCompleto).

# Archivado automático
(AplicarCambioSituacion / Situacion_AfterUpdate): Al cambiar Situacion a "Dispensado", "No se dispensa" o "Pedido guardado", se exige rellenar Observaciones si no se dispensa, se pide confirmación (revirtiendo a OldValue si se cancela o falta Observaciones/cantidad), se solicita cantidad solo en "Dispensado", se guarda el registro, se ejecuta AnexarHistorico, se actualiza [Cantidad dispensada] en Historico por ID, se ejecuta EliminarRegistro, se refresca con ActualizarPedidosPlanta y se vuelve al primer registro (acFirst).

# Botones y refresco
Botón de cancelar (Me.Undo + Requery + acFirst), guardado simple y refresco periódico con Form_Timer (respetando Me.Dirty) o macro paso a paso (usando ; en expresiones de Access en español).

# Búsqueda en histórico (btnBuscar_Click)
Filtra HistoricoCompleto por coincidencia exacta en NHC y/o [Solicitud Athos], y por texto libre (LIKE "*...*") en [Medicamento].
