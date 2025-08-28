# colecciones-de-java-
import java.util.*;

public class BuggyActividadCorregida {

    public static void main(String[] args) {

        // LISTA de nombres
        List<String> nombres = new ArrayList<>();
        nombres.add("Ana");
        nombres.add("Luis");
        nombres.add("Ana");

        // Validación antes de acceder a índice
        int index = 2;
        if (index < nombres.size()) {
            System.out.println("Elemento en posición " + index + ": " + nombres.get(index));
        } else {
            System.out.println("Índice fuera de rango.");
        }

        // Comparación de cadenas con equals
        String buscado = new String("Ana");
        if (buscado.equals("Ana")) {
            System.out.println("Encontrado");
        }

        // MAPA de teléfonos
        Map<String, String> telefonos = new HashMap<>();
        if (!telefonos.containsKey("Ana")) {
            telefonos.put("Ana", "0991111111");
        }
        telefonos.put("Luis", "0992222222");

        // Intento de sobrescribir "Ana"
        if (!telefonos.containsKey("Ana")) {
            telefonos.put("Ana", "0993333333");
        } else {
            System.out.println("La clave 'Ana' ya existe. No se sobrescribe.");
        }

        // Validación al obtener clave inexistente
        String telefonoBea = telefonos.get("Bea");
        if (telefonoBea != null) {
            System.out.println("Bea: " + telefonoBea);
        } else {
            System.out.println("No existe teléfono para Bea.");
        }

        // SET de inscritos (no permite duplicados lógicos)
        Set<Alumno> inscritos = new HashSet<>();
        inscritos.add(new Alumno(1, "Ana"));
        inscritos.add(new Alumno(2, "Luis"));
        inscritos.add(new Alumno(1, "Ana")); // duplicado lógico

        System.out.println("Tamaño del Set: " + inscritos.size());
        System.out.println(inscritos);
    }
}

class Alumno {
    int id;
    String nombre;

    Alumno(int id, String nombre) {
        this.id = id;
        this.nombre = nombre;
    }

    @Override
    public String toString() {
        return "Alumno{id=" + id + ", nombre='" + nombre + "'}";
    }

    // Para evitar duplicados lógicos en HashSet
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Alumno)) return false;
        Alumno alumno = (Alumno) o;
        return id == alumno.id && Objects.equals(nombre, alumno.nombre);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id, nombre);
    }
}
