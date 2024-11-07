### Problema: Rutas Aéreas y Costos Mínimos

**Descripción del Problema:**
Eres parte de un equipo de análisis de tráfico aéreo en Colombia y se te ha encomendado la tarea de optimizar las rutas aéreas entre los aeropuertos más importantes del país. Debes desarrollar una solución que permita a los pasajeros encontrar las mejores rutas entre dos aeropuertos en términos de distancia y costo.

**Aeropuertos a Considerar:**
- Bogotá (El Dorado)
- Medellín (José María Córdova)
- Rionegro (José María Córdova)
- Chachagüí (Nariño)
- Manizales (La Nubia)
- Pereira (Matecaña)
- San Andrés (Gustavo Rojas Pinilla)
- Santa Marta (Simón Bolívar)
- Cartagena (Rafael Núñez)

**Entradas del Problema:**
1. Una lista de conexiones de vuelos entre los aeropuertos, donde cada conexión tiene una distancia y un costo asociado.
2. Un aeropuerto de origen y un aeropuerto de destino ingresados por el usuario.
3. Un día específico para consultar los costos de los vuelos.

**Requerimientos:**
1. Implementar un grafo que represente los aeropuertos y las conexiones entre ellos.
2. Escribir una función que permita consultar la ruta más corta (en términos de distancia) entre el aeropuerto de origen y destino.
3. Escribir otra función que permita consultar la ruta de menor costo entre el mismo par de aeropuertos.
4. Consultar el costo más alto para un día específico entre las 8 a.m. y 6 p.m., considerando solo los vuelos disponibles en ese rango horario.
5. Usar valores reales para las distancias y costos, consultando fuentes confiables como los sitios web de aerolíneas y plataformas de vuelos.

**Salidas del Problema:**
1. Mostrar la ruta de menor distancia, incluyendo la secuencia de aeropuertos y la distancia total.
2. Mostrar la ruta de menor costo, incluyendo la secuencia de aeropuertos y el costo total.
3. Mostrar el costo más alto para el día específico consultado entre las 8 a.m. y 6 p.m.

**Ejemplo de Entrada:**
```
Origen: Bogotá
Destino: San Andrés
Día: 2024-11-15
```

**Ejemplo de Salida:**
```
Ruta de menor distancia: Bogotá -> Medellín -> San Andrés
Distancia total: 650 km

Ruta de menor costo: Bogotá -> Pereira -> San Andrés
Costo total: $200.000

Costo más alto del día 2024-11-15 entre 8 a.m. y 6 p.m.: $500.000
