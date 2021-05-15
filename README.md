# proyecto1
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System;
using System.IO;

namespace proyectodecatedra
{
    class Program
    {

        static StreamReader leer;
        static StreamWriter escribir;
        static void Main(string[] args)
        {
            int opc = 0;

            do
            {
                Console.WriteLine("1-Ingresar datos");
                Console.WriteLine("2-Mostrar datos");
                Console.WriteLine("3-Buscar datos");
                Console.WriteLine("4-Salir");
                Console.WriteLine("Seleccione una opción");

                opc = Int32.Parse(Console.ReadLine());
                Console.Clear();
                if (opc == 1) agregar();
                if (opc == 2) mostrar();
                if (opc == 3) buscar();

            } while (opc != 4);
        }

        private static void buscar()
        {
            Console.Clear();
            leer = new StreamReader("C:\\Windows\\registro\\registro.txt");
            String registro = "";
            char[] caracter = new char[1];
            caracter[0] = ',';
            String dui = "";
            Console.WriteLine("Digite DUI a buscar:");
            dui = Console.ReadLine();
            bool encontro = false;
            while ((registro = leer.ReadLine()) != null)
            {
                String[] datos = registro.Split(caracter);
                if (dui == datos[0])
                {
                    Console.WriteLine("**** REGISTRO ENCONTRADO*****");
                    Console.WriteLine($"DUI : {datos[0]}");
                    Console.WriteLine($"NOMBRE : {datos[1]}");
                    Console.WriteLine($"VEHICULO : {datos[2]}");
                    Console.WriteLine($"COSTO : {datos[3]}");

                    Console.WriteLine("**********************");
                    encontro = true;

                }
                if (encontro == false)
                {
                    Console.WriteLine("**** REGISTRO NO ENCONTRADO*****");
                }


                leer.Close();
            }
        }
        private static void mostrar()
        {
            Console.Clear();
            leer = new StreamReader("C:\\Windows\\registro\\registro.txt");
            String registro = "";
            char[] caracter = new char[1];
            caracter[0] = ',';

            while ((registro = leer.ReadLine()) != null)
            {
                String[] datos = registro.Split(caracter);
                Console.WriteLine("**********************");
                Console.WriteLine($"DUI : {datos[0]}");
                Console.WriteLine($"NOMBRE : {datos[1]}");
                Console.WriteLine($"VEHICULO : {datos[2]}");
                Console.WriteLine($"COSTO : {datos[3]}");
                Console.WriteLine("**********************");
            }
            leer.Close();
        }

        private static void agregar()
        {
            Console.Clear();
            escribir = new StreamWriter("C:\\Windows\\registro\\registro.txt", true);
            Persona p = new Persona();
            Console.WriteLine("Digite DUI");
            p.DUI = Console.ReadLine();
            Console.WriteLine("Digite NOMBRE");
            p.NOMBRE = Console.ReadLine();
            Console.WriteLine("Digite VEHICUL0");
            p.VEHICULO = Console.ReadLine();
            Console.WriteLine("Digite COSTO DE REPARACION");
            p.COSTO = Console.ReadLine();
            String registro = $"{p.DUI},{p.NOMBRE},{p.VEHICULO}," +
                $"{p.COSTO}";

            escribir.WriteLine(registro);
            escribir.Close();
        }



        struct Persona
        {
            public String DUI, NOMBRE, VEHICULO, COSTO;
        }
    }
}
