Alumno: Aldo Raul Martinez Choque

Estilos de progmacion que fueron aplicados en api/index.js y Data/Repositorio/UserRepository.js

07-code-golf: Simplificamos la función getCandidatos eliminando comentarios y utilizando la sintaxis de funciones de flecha de forma más concisa.
```bash
const res = await axios.get(`/api/candidatos/?page=${page}&pageSize=${pageSize}`);
const data = res.data[0].sort((a, b) => a.nombre_partido.localeCompare(b.nombre_partido));
setCandidatos((prevCandidatos) => [...prevCandidatos, ...data]);
```
14-abstract-things: Los datos de candidatos se representan como objetos con propiedades como:
```bash
nombre, apellido, cargo, y nombre_partido.
```
22-tantrum: Se maneja el posible error en la llamada a la API usando un bloque try-catch para capturar y manejar el error.
```bash
  const getCandidatos = async () => {
    try {
      const res = await axios.get(`/api/candidatos/?page=${page}&pageSize=${pageSize}`);
      const data = res.data[0].sort((a, b) => a.nombre_partido.localeCompare(b.nombre_partido));
      setCandidatos((prevCandidatos) => [...prevCandidatos, ...data]);
    } catch (error) {
      console.error("Error fetching candidates:", error);
      
    }
  };
```
28-lazy-rivers: Implementamos paginación para cargar candidatos en lotes más pequeños. Ahora, la función getCandidatos carga candidatos en función del valor de page, lo que permite cargar candidatos en lotes en lugar de cargarlos todos a la vez.
```bash
app.get('/api/candidatos/', (req, res) => {
  const { page, pageSize } = req.query;
});

// Frontend IndexPage component
import { useState, useEffect } from 'react';
import axios from 'axios';

export default function IndexPage() {
  const [candidatos, setCandidatos] = useState([]);
  const [page, setPage] = useState(1);
  const pageSize = 10;

  useEffect(() => {
    getCandidatos();
  }, [page]);

  const getCandidatos = async () => {
    try {
      const res = await axios.get(`/api/candidatos/?page=${page}&pageSize=${pageSize}`);
      const data = res.data[0].sort((a, b) => a.nombre_partido.localeCompare(b.nombre_partido));
      setCandidatos((prevCandidatos) => [...prevCandidatos, ...data]);
    } catch (error) {
      console.error("Error fetching candidates:", error);
      // Handle the error or show a friendly message to the user.
    }
  };

  // .el resto de codigo
}

```
36-dense-shallow-under-control:
Este estilo implica escribir código conciso y expresivo mientras se mantiene bajo control, lo que significa que el código es fácil de entender y mantener. El código de UserRepository sigue esta línea, donde las funciones son claras y están bien organizadas. También se manejan los errores de manera controlada mediante el uso de try-catch para no comprometer el flujo de la aplicación en caso de que ocurra un error en la comunicación con la API.

```bash
import axios from 'axios';

class UserRepository {
    static async getUsers({username,password}) {
        try {
            const user = {
                username:username,
                password:password,
            }
            const response = await axios.post('/api/services/login',user);
            return response;
        } catch (error) {
            console.error('Error al obtener usuarios desde la base de datos:', error);
            throw error;
        }
    }

    static async getUserById(id) {
        try {
            const response = await axios.get(`/api/users/${id}`);
            return response.data;
        } catch (error) {
            console.error(`Error al obtener el usuario con ID ${id}:`, error);
            throw error;
        }
    }

    // Otras operaciones de acceso a la base de datos utilizando Axios
}

export default UserRepository;
```
