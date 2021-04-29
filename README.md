# Proyecto- Tienda de Computadoras
Proyecto Introducción a la Programación 
package proyectofinal;

public class TComputadoras {

    public static void main(String[] args) {
        Registros tienda = new Registros();
        tienda.Menu_principal();
    }

}
package proyectofinal;

import javax.swing.JOptionPane;

public class Registros {

    Cliente comprador = new Cliente();
    Cajas comprado = new Cajas();
    Num_tienda TI = new Num_tienda();
    Producto pr = new Producto();

    int Compra = 0, cont = 0, con;

    public void Menu_principal() {
        int Tienda;

        do {
            Tienda = Integer.parseInt(JOptionPane.showInputDialog("Proyecto de Tienda de computadoras.\n"
                    + "\nDigite la accion que desea llevar a cabo."
                    + "\n1. Registrarse."
                    + "\n2. Comprar."
                    + "\n3. Buscar productos."
                    + "\n4. Informacion cliente."
                    + "\n5. Tiendas disponibles."
                    + "\n6. Ultima compra realizada."
                    + "\n0. Salir."));

            switch (Tienda) {
                case 1:
                    Registro();
                    break;
                case 2:
                    Compras();
                    break;
                case 3:
                    pr.promociones();
                    break;
                case 4:
                    if (cont == 0) {
                        JOptionPane.showMessageDialog(null, "Aun no hay informacion cliente.");
                    } else {
                        comprador.informacionCliente();
                    }
                    break;
                case 5:
                    int opt = Integer.parseInt(JOptionPane.showInputDialog("1. Informacion de todas las tiendas."
                            + "\n2. Buscar con una ubicacion especifica."));
                    switch (opt) {
                        case 1:
                            TI.buscarTienda();
                            break;
                        case 2:
                            TI.ubicacion();
                            break;
                    }
                    break;
                case 6:
                    Facturas();
                    break;
            }
        } while (Tienda != 0);
    }

    public void Registro() {
        if (cont < 1) {
            comprador.setNombre(JOptionPane.showInputDialog("Ingrese su nombre."));
            comprador.setNumero_de_cedula(JOptionPane.showInputDialog("Ingrese su numero de cedula."));
            comprador.setNumero_de_telefono(Integer.parseInt(JOptionPane.showInputDialog("Ingrese su numero telefonico.")));
            comprador.setCorreo(JOptionPane.showInputDialog("Ingrese su correo electronico."));

            Compra = Integer.parseInt(JOptionPane.showInputDialog("Los clientes usuales cuentan con un credito inicial"
                    + "\nde ₡75.000. Al comprar una membresia VIP su credito"
                    + "\ninicial sera de ₡175.000.\n\n"
                    + "\n¿Desea adquirir una membresia VIP?"
                    + "\n1. Si."
                    + "\n2. No"));
            switch (Compra) {
                case 1:
                    comprador.setMembresiaVIP("Activa.");
                    comprador.setCredito(175000);
                    break;
                case 2:
                    comprador.setMembresiaVIP("No posee.");
                    comprador.setCredito(75000);
                    break;
            }
            cont++;
            comprador.setTarjeta(cont);

            JOptionPane.showMessageDialog(null, "¡¡Tus datos han sido agregados de manera exitosa!!\n"
                    + "\nNombre: " + comprador.getNombre()
                    + "\nNumero de cedula: " + comprador.getNumero_de_cedula()
                    + "\nNumero de telefono: " + comprador.getNumero_de_telefono()
                    + "\nCorreo electronico: " + comprador.getCorreo()
                    + "\nMembresia VIP: " + comprador.getMembresiaVIP()
                    + "\nSaldo credito: ₡" + comprador.getCredito()
                    + "\n\nSu numero de tarjeta de membresia VIP es:  " + comprador.getTarjeta());
        } else {
            JOptionPane.showMessageDialog(null, "Cupo de clientes lleno.");
        }
    }

    public void Compras() {
        int Codigo_del_producto = Integer.parseInt(JOptionPane.showInputDialog("Escriba el codigo del producto que desea comprar."));
        if (Codigo_del_producto < 9001 || Codigo_del_producto > 9007) {
            JOptionPane.showMessageDialog(null, "Producto no encontrado.");
        }

        switch (Codigo_del_producto) {
            case 9001:
                int op = Integer.parseInt(JOptionPane.showInputDialog("Articulo: " + pr.getCategoria1() + ""
                        + "\nPrecio: " + pr.getPrecio1() + "\n\n¿Desea comprar este producto?"
                        + "\n1. Si\n2. No"));
                if (op == 1) {
                    int ID_cliente = Integer.parseInt(JOptionPane.showInputDialog("Escriba su numero de tarjeta de membresia VIP."
                            + "\n\nSi no sabe cual es, digite 0 y seleccione"
                            + "\nla opcion 4 en el menu principal."));

                    if (ID_cliente == 1) {
                        con = Integer.parseInt(JOptionPane.showInputDialog("Cliente:  " + comprador.getNombre()
                                + "\nCedula:  " + comprador.getNumero_de_cedula()
                                + "\nCredito actual de:  " + comprador.getCredito()
                                + "\n\n¿Los datos son correctos?"
                                + "\n1. Continuar."
                                + "\n2. Reintentar."
                                + "\n0. Salir"));
                    }
                    if (con == 1) {
                        JOptionPane.showMessageDialog(null, "¡¡Tu compra ha sido realizada con exito!!"
                                + "\n\n**   Factura a nombre de: " + comprador.getNombre()
                                + "\n**   Cedula: " + comprador.getNumero_de_cedula()
                                + "\n**   Correo: " + comprador.getCorreo()
                                + "\n**   Membresia VIP: " + comprador.getMembresiaVIP()
                                + "\n\n**   Articulo adquirido: " + pr.getCategoria1()
                                + "\n**   Codigo del articulo: " + pr.getCodigo_de_barras1()
                                + "\n**   Pago total de: " + pr.getPrecio1());
                    }

                    if (ID_cliente != 1 && ID_cliente != 0) {
                        JOptionPane.showMessageDialog(null, "cliente no registrado.");
                    }
                }
                break;

            case 9002:
                break;

            case 9003:
                break;

            case 9004:
                break;

            case 9005:
                break;

            case 9006:
                break;

            case 9007:
                break;

        }
    }

    public void Facturas() {
        comprado.Vender();
    }
}
package proyectofinal;

import javax.swing.JOptionPane;

public class Producto {

    private String Categoria1;
    private int Codigo_de_barras1;
    private int Precio1;
    private String Categoria2;
    private int Codigo_de_barras2;
    private int Precio2;
    private String Categoria3;
    private int Codigo_de_barras3;
    private int Precio3;
    private String Categoria4;
    private int Codigo_de_barras4;
    private int Precio4;
    private String Categoria5;
    private int Codigo_de_barras5;
    private int Precio5;
    private String Categoria6;
    private int Codigo_de_barras6;
    private int Precio6;
    private String Categoria7;
    private int Codigo_de_barras7;
    private int Precio7;

    public Producto() {
        Categoria1 = "Computadora Dell 990 SFF.";
        Codigo_de_barras1 = 9001;
        Categoria2 = "Teclado inalámbrico Dell.";
        Codigo_de_barras2 = 9002;
        Categoria3 = "Monitor Razer 280hz.";
        Codigo_de_barras3 = 9003;
        Categoria4 = "Audifonos Inalámbricos Razer.";
        Codigo_de_barras4 = 9004;
        Categoria5 = "Mousepad ASUS RGB.";
        Codigo_de_barras5 = 9005;
        Categoria6 = "Mouse inalámbrico ASUS.";
        Codigo_de_barras6 = 9006;
        Categoria7 = "Silla gaming Intimate WM Heart";
        Codigo_de_barras7 = 9007;

        Precio1 = 85000;
        Precio2 = 2500;
        Precio3 = 75000;
        Precio4 = 35000;
        Precio5 = 23000;
        Precio6 = 13500;
        Precio7 = 160000;
    }

    public String getCategoria1() {
        return Categoria1;
    }

    public void setCategoria1(String Categoria1) {
        this.Categoria1 = Categoria1;
    }

    public int getCodigo_de_barras1() {
        return Codigo_de_barras1;
    }

    public void setCodigo_de_barras1(int Codigo_de_barras1) {
        this.Codigo_de_barras1 = Codigo_de_barras1;
    }

    public int getPrecio1() {
        return Precio1;
    }

    public void setPrecio1(int Precio1) {
        this.Precio1 = Precio1;
    }

    public String getCategoria2() {
        return Categoria2;
    }

    public void setCategoria2(String Categoria2) {
        this.Categoria2 = Categoria2;
    }

    public int getCodigo_de_barras2() {
        return Codigo_de_barras2;
    }

    public void setCodigo_de_barras2(int Codigo_de_barras2) {
        this.Codigo_de_barras2 = Codigo_de_barras2;
    }

    public int getPrecio2() {
        return Precio2;
    }

    public void setPrecio2(int Precio2) {
        this.Precio2 = Precio2;
    }

    public String getCategoria3() {
        return Categoria3;
    }

    public void setCategoria3(String Categoria3) {
        this.Categoria3 = Categoria3;
    }

    public int getCodigo_de_barras3() {
        return Codigo_de_barras3;
    }

    public void setCodigo_de_barras3(int Codigo_de_barras3) {
        this.Codigo_de_barras3 = Codigo_de_barras3;
    }

    public int getPrecio3() {
        return Precio3;
    }

    public void setPrecio3(int Precio3) {
        this.Precio3 = Precio3;
    }

    public String getCategoria4() {
        return Categoria4;
    }

    public void setCategoria4(String Categoria4) {
        this.Categoria4 = Categoria4;
    }

    public int getCodigo_de_barras4() {
        return Codigo_de_barras4;
    }

    public void setCodigo_de_barras4(int Codigo_de_barras4) {
        this.Codigo_de_barras4 = Codigo_de_barras4;
    }

    public int getPrecio4() {
        return Precio4;
    }

    public void setPrecio4(int Precio4) {
        this.Precio4 = Precio4;
    }

    public String getCategoria5() {
        return Categoria5;
    }

    public void setCategoria5(String Categoria5) {
        this.Categoria5 = Categoria5;
    }

    public int getCodigo_de_barras5() {
        return Codigo_de_barras5;
    }

    public void setCodigo_de_barras5(int Codigo_de_barras5) {
        this.Codigo_de_barras5 = Codigo_de_barras5;
    }

    public int getPrecio5() {
        return Precio5;
    }

    public void setPrecio5(int Precio5) {
        this.Precio5 = Precio5;
    }

    public String getCategoria6() {
        return Categoria6;
    }

    public void setCategoria6(String Categoria6) {
        this.Categoria6 = Categoria6;
    }

    public int getCodigo_de_barras6() {
        return Codigo_de_barras6;
    }

    public void setCodigo_de_barras6(int Codigo_de_barras6) {
        this.Codigo_de_barras6 = Codigo_de_barras6;
    }

    public int getPrecio6() {
        return Precio6;
    }

    public void setPrecio6(int Precio6) {
        this.Precio6 = Precio6;
    }

    public String getCategoria7() {
        return Categoria7;
    }

    public void setCategoria7(String Categoria7) {
        this.Categoria7 = Categoria7;
    }

    public int getCodigo_de_barras7() {
        return Codigo_de_barras7;
    }

    public void setCodigo_de_barras7(int Codigo_de_barras7) {
        this.Codigo_de_barras7 = Codigo_de_barras7;
    }

    public int getPrecio7() {
        return Precio7;
    }

    public void setPrecio7(int Precio7) {
        this.Precio7 = Precio7;
    }

    public void promociones() {
        JOptionPane.showMessageDialog(null, "***********   Productos a la venta en todas las tiendas   ***********\n\n\n"
                + Categoria1 + ".                                 Codigo " + Codigo_de_barras1 + ".  Precio: ₡" + Precio1 + "\n"
                + Categoria2 + ".                                   Codigo " + Codigo_de_barras2 + ".  Precio: ₡" + Precio2 + "\n"
                + Categoria3 + ".                             Codigo " + Codigo_de_barras3 + ".  Precio: ₡" + Precio3 + "\n"
                + Categoria4 + ".         Codigo " + Codigo_de_barras4 + ".  Precio: ₡" + Precio4 + "\n"
                + Categoria5 + ".                                                  Codigo " + Codigo_de_barras5 + ".  Precio: ₡" + Precio5 + "\n"
                + Categoria6 + ".                               Codigo " + Codigo_de_barras6 + ".  Precio: ₡" + Precio6 + "\n"
                + Categoria7 + ".                            Codigo " + Codigo_de_barras7 + ".  Precio: ₡" + Precio7);
    }

}
package proyectofinal;

import javax.swing.JOptionPane;

public class Num_tienda {

    private String Localizacion1;
    private String Horario1;
    private String Localizacion2;
    private String Horario2;
    private String Localizacion3;
    private String Horario3;
    private String Localizacion4;
    private String Horario4;
    private String ID_de_tienda1;
    private String ID_de_tienda2;
    private String ID_de_tienda3;
    private String ID_de_tienda4;

    public Num_tienda() {
        Localizacion1 = "Heredia";
        Horario1 = "9:00am - 9:00pm";
        Localizacion2 = "Alajuela";
        Horario2 = "8:00am - 7:00pm";
        Localizacion3 = "Escazú";
        Horario3 = "11:00am - 2:00pm";
        Localizacion4 = "Guanacaste";
        Horario4 = "7:00am - 6:00pm";
        ID_de_tienda1 = "TI#12";
        ID_de_tienda2 = "TI#13";
        ID_de_tienda3 = "TI#19";
        ID_de_tienda4 = "TI#15";
    }

    public void buscarTienda() {

        JOptionPane.showMessageDialog(null, "Todas las tiendas habilitadas son:\n"
                + "\nTienda " + ID_de_tienda1 + ".  Ubicacion: " + Localizacion1 + ".          Horario: " + Horario1 + "."
                + "\nTienda " + ID_de_tienda2 + ".  Ubicacion: " + Localizacion2 + ".   Horario: " + Horario2 + "."
                + "\nTienda " + ID_de_tienda3 + ".  Ubicacion: " + Localizacion3 + ".     Horario: " + Horario3 + "."
                + "\nTienda " + ID_de_tienda4 + ".  Ubicacion: " + Localizacion4 + ".       Horario: " + Horario4 + ".");
    }

    public void ubicacion() {

        String location = JOptionPane.showInputDialog("Escriba la zona que desea consultar.");

        if (location.equals("heredia") || location.equals("Heredia")) {
            JOptionPane.showMessageDialog(null, "Tienda " + ID_de_tienda1 + ".  Ubicacion: " + Localizacion1 + ".  Horario: " + Horario1 + ".");
        }
        if (location.equals("alajuela")) {
            JOptionPane.showMessageDialog(null, "Tienda " + ID_de_tienda2 + ".  Ubicacion: " + Localizacion2 + ".  Horario: " + Horario2 + ".");
        }
        if (location.equals("escazú")) {
            JOptionPane.showMessageDialog(null, "Tienda " + ID_de_tienda3 + ".  Ubicacion: " + Localizacion3 + ".  Horario: " + Horario3 + ".");
        }
        if (location.equals("guanacaste")) {
            JOptionPane.showMessageDialog(null, "Tienda " + ID_de_tienda4 + ".  Ubicacion: " + Localizacion4 + ".  Horario: " + Horario4 + ".");
        }
        if (!location.equals("heredia") && !location.equals("Heredia") && !location.equals("Alajuela") && !location.equals("Escazú") && !location.equals("Guanacaste")) {
            JOptionPane.showMessageDialog(null, "No se encuentra ninguna tienda"
                    + "\nen esta ubicacion.");
        }
    }

    public String getLocalizacion1() {
        return Localizacion1;
    }

    public void setLocalizacion1(String Localizacion1) {
        this.Localizacion1 = Localizacion1;
    }

    public String getHorario1() {
        return Horario1;
    }

    public void setHorario1(String Horario1) {
        this.Horario1 = Horario1;
    }

    public String getLocalizacion2() {
        return Localizacion2;
    }

    public void setLocalizacion2(String Localizacion2) {
        this.Localizacion2 = Localizacion2;
    }

    public String getHorario2() {
        return Horario2;
    }

    public void setHorario2(String Horario2) {
        this.Horario2 = Horario2;
    }

    public String getLocalizacion3() {
        return Localizacion3;
    }

    public void setLocalizacion3(String Localizacion3) {
        this.Localizacion3 = Localizacion3;
    }

    public String getHorario3() {
        return Horario3;
    }

    public void setHorario3(String Horario3) {
        this.Horario3 = Horario3;
    }

    public String getLocalizacion4() {
        return Localizacion4;
    }

    public void setLocalizacion4(String Localizacion4) {
        this.Localizacion4 = Localizacion4;
    }

    public String getHorario4() {
        return Horario4;
    }

    public void setHorario4(String Horario4) {
        this.Horario4 = Horario4;
    }

    public String getID_de_tienda1() {
        return ID_de_tienda1;
    }

    public void setID_de_tienda1(String ID_de_tienda1) {
        this.ID_de_tienda1 = ID_de_tienda1;
    }

    public String getID_de_tienda2() {
        return ID_de_tienda2;
    }

    public void setID_de_tienda2(String ID_de_tienda2) {
        this.ID_de_tienda2 = ID_de_tienda2;
    }

    public String getID_de_tienda3() {
        return ID_de_tienda3;
    }

    public void setID_de_tienda3(String ID_de_tienda3) {
        this.ID_de_tienda3 = ID_de_tienda3;
    }

    public String getID_de_tienda4() {
        return ID_de_tienda4;
    }

    public void setID_de_tienda4(String ID_de_tienda4) {
        this.ID_de_tienda4 = ID_de_tienda4;
    }
}
package proyectofinal;

public class Locales {

    private String Ubic;
    private String Comentarios;

    public Locales() {
        Ubic = "";
        Comentarios = "";
    }

    public String getUbic() {
        return Ubic;
    }

    public void setUbic(String Ubic) {
        this.Ubic = Ubic;
    }

    public String getComentarios() {
        return Comentarios;
    }

    public void setComentarios(String Comentarios) {
        this.Comentarios = Comentarios;
    }

}

package proyectofinal;

import javax.swing.JOptionPane;

public class Cliente {

    private String Numero_de_cedula;
    private String Nombre;
    private String MembresiaVIP;
    private int Credito;
    private String Correo;
    private int Numero_de_telefono;
    private int Tarjeta;

    public Cliente() {
        Numero_de_cedula = "";
        Nombre = "";
        MembresiaVIP = "";
        Credito = 0;
        Correo = "";
        Numero_de_telefono = 0;
        Tarjeta = 0;
    }

    public String getNumero_de_cedula() {
        return Numero_de_cedula;
    }

    public void setNumero_de_cedula(String Numero_de_cedula) {
        this.Numero_de_cedula = Numero_de_cedula;
    }

    public String getNombre() {
        return Nombre;
    }

    public void setNombre(String Nombre) {
        this.Nombre = Nombre;
    }

    public String getMembresiaVIP() {
        return MembresiaVIP;
    }

    public void setMembresiaVIP(String Membresia) {
        this.MembresiaVIP = Membresia;
    }

    public int getCredito() {
        return Credito;
    }

    public void setCredito(int Credito) {
        this.Credito = Credito;
    }

    public String getCorreo() {
        return Correo;
    }

    public void setCorreo(String Correo) {
        this.Correo = Correo;
    }

    public int getNumero_de_telefono() {
        return Numero_de_telefono;
    }

    public void setNumero_de_telefono(int Numero_de_telefono) {
        this.Numero_de_telefono = Numero_de_telefono;
    }

    public int getTarjeta() {
        return Tarjeta;
    }

    public void setTarjeta(int Tarjeta) {
        this.Tarjeta = Tarjeta;
    }

    public void informacionCliente() {
        JOptionPane.showMessageDialog(null,
                "****************Informacion cliente***************\n\n\n"
                + "Cliente 1.\n"
                + "\nNombre: " + Nombre
                + "\nNumero de cedula: " + Numero_de_cedula
                + "\nNumero de telefono: " + Numero_de_telefono
                + "\nMembresia: " + MembresiaVIP
                + "\nCorreo: " + Correo
                + "\nNumero tarjeta VIP: " + Tarjeta
                + "\nCredito es de: ₡" + Credito);

    }
}
package proyectofinal;

import javax.swing.JOptionPane;

public class Cajas {

    Producto pro = new Producto();

    int con = 0, ID_cliente = 0;

    public void Vender() {
        JOptionPane.showMessageDialog(null, "El ultimo artefacto vendido fue:\n\n"
                + "\n\n**   Articulo adquirido: " + pro.getCategoria1()
                + "\n**   Codigo del articulo: " + pro.getCodigo_de_barras1()
                + "\n**   Pago total de: " + pro.getPrecio1());
    }

}
package proyectofinal;

import javax.swing.JOptionPane;

public class Almacen {

    private String[] products1;
    private String[] products2;
    private String[] products3;
    private int[] precio1;
    private int[] precio2;
    private int[] precio3;
    private String[] proveedor;

    public Almacen() {
        products1 = new String[2];
        products2 = new String[2];
        products3 = new String[2];
        precio1 = new int[2];
        precio2 = new int[2];
        precio3 = new int[2];
        proveedor = new String[3];

        products1[0] = "Computadora Dell 990 SFF.";
        precio1[0] = 85000;
        proveedor[0] = "Dell.";
        products1[1] = "Teclado inalámbrico Dell.";
        precio1[1] = 2500;
        products2[0] = "Monitor Razer 280hz.";
        precio2[0] = 75000;
        proveedor[1] = "Razer.";
        products2[1] = "Audifonos Inalámbricos Razer.";
        precio2[1] = 25000;
        products3[0] = "Mousepad ASUS RGB.";
        precio3[23000] = 0;
        proveedor[2] = "ASUS.";
        products3[1] = "Mouse inalámbrico ASUS.";
        precio3[1] = 13500;
    }

    public String[] getProductos1() {
        return products1;
    }

    public void setProductos1(String[] productos1) {
        this.products1 = productos1;
    }

    public String[] getProductos2() {
        return products2;
    }

    public void setProductos2(String[] productos2) {
        this.products2 = productos2;
    }

    public String[] getProductos3() {
        return products3;
    }

    public void setProductos3(String[] productos3) {
        this.products3 = productos3;
    }

    public int[] getPrecio1() {
        return precio1;
    }

    public void setPrecio1(int[] precio1) {
        this.precio1 = precio1;
    }

    public int[] getPrecio2() {
        return precio2;
    }

    public void setPrecio2(int[] precio2) {
        this.precio2 = precio2;
    }

    public int[] getPrecio3() {
        return precio3;
    }

    public void setPrecio3(int[] precio3) {
        this.precio3 = precio3;
    }

    public String[] getProveedor() {
        return proveedor;
    }

    public void setProveedor(String[] proveedor) {
        this.proveedor = proveedor;
    }

    public void cantidades() {
        int selec = 0;

        do {
            selec = Integer.parseInt(JOptionPane.showInputDialog("Seleccione la marca del proveedor que desea adquirir.\n\n"
                    + "1. " + proveedor[0]
                    + "\n2. " + proveedor[1]
                    + "\n3. " + proveedor[2]));

            switch (selec) {
                case 1:
                    JOptionPane.showMessageDialog(null, "Proveedor: " + proveedor[0]
                            + "\nArticulo: " + products1[0] + "\nPrecio: " + precio1[0]
                            + "\n\nArticulo: " + products1[1] + "\nPrecio: " + precio1[1]);
                    break;
                case 2:
                    break;
                case 3:
                    break;
                case 0:
                    break;
                default:
                    JOptionPane.showMessageDialog(null, "Seleccione una opcion valida.");
            }
        } while (selec != 0);
    }
}
package proyectofinal;

public class Trabajador {

    private String Nombre;
    private String ID;
    private int Num_Gafete;

    public Trabajador() {
        Nombre = "";
        ID = "";
        Num_Gafete = 0;
    }

    public String getNombre() {
        return Nombre;
    }

    public void setNombre(String Nombre) {
        this.Nombre = Nombre;
    }

    public String getID() {
        return ID;
    }

    public void setID(String ID) {
        this.ID = ID;
    }

    public int getNum_Gafete() {
        return Num_Gafete;
    }

    public void setNum_Gafete(int Num_Gafete) {
        this.Num_Gafete = Num_Gafete;
    }

}
