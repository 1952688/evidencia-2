1
def Menu():


2
    print("Menu Principal")


3
    print("[1] Registro de Servicio")


4
    print("[2] Consulta de Folio por Numero")


5
    print("[3] Consulta de Servicios por Fecha")


6
    print("[4] Consulta de Folios por Fechas")


7
    print("[5] Salir")


8



9
    opcion = int(input("Elija una opción: "))


10
    if opcion==1:


11
        print("****************REGISTRO DE SERVICIO********************")        


12
        NuevoFolio()


13
    elif opcion ==2:


14
        ConsultaServiciosFolio()


15
    elif opcion ==3:


16
        ConsultaServiciosFecha()


17
    elif opcion==4:


18
        ConsultaFolioEmp()


19
    elif opcion==5:


20
        exit


21
    else:


22
        print("Intente de nuevo , seleccione 1-4")


23
        Menu()


24



25
def NuevoFolio():


26
    


27
    opcion = input("Desea agregar un equipo al folio(Y/N): ")


28
    if opcion=="Y":


29
        AgregarEquipo()


30
    elif opcion=="N":


31
        global n_folio


32
        print("Su numero de folio es: " + str(n_folio))


33
        exit


34
    else:


35
        print("Teclear Y para agregar folio, N para terminar folio")


36
        NuevoFolio()


37



38
def CreaNuevoFolio():


39
    import csv, operator


40
    with open('c:\\registro\FoliosServicio.csv') as csvarchivo:


41
        entrada = csv.reader(csvarchivo)


42
        sortedlist = sorted(entrada, key=operator.itemgetter(0), reverse=False)


43
        maxVal = []


44
        for row in sortedlist:


45
            maxVal.append(row[0])


46
    if contador == 1:


47
        siguiente = 1


48
        siguiente = siguiente + int(max(maxVal))


49
        return siguiente


50
    else:


51
        siguiente = 0


52
        siguiente = siguiente + int(max(maxVal))


53
        return siguiente


54



55
def AgregarEquipo():


56
    


57
    global contador


58
    global n_folio


59
    import csv, operator


60
    from datetime import datetime


61
    


62
    archivo_folios = open('c:\\registro\FoliosServicio.csv', 'a', newline='')


63



64
    folio = CreaNuevoFolio()


65
    


66
    fecha_folio = str(datetime.today().strftime('%Y-%m-%d'))


67
    nombre_cliente = input("Teclee el nombre del cliente: ")


68
    descripcion_servicio = input("Teclee el servicio a proporcionar: ")
#se preparan los datos para ser ligados en la estructura de datos

69
    descripcion_equipo = input("Teclee descripcion del equipo: ")


70
    costo_servicio = float(input("Teclee el costo del servicio: "))


71
    iva = float((costo_servicio * .16))


72
    precio_total=float((iva + costo_servicio))


73



74
    datos = [folio, fecha_folio, nombre_cliente, descripcion_servicio, descripcion_equipo, costo_servicio, iva, precio_total]
#se crea tupla con datos a guardar

75
    salida = csv.writer(archivo_folios)


76
    salida.writerow(datos)


77



78
    archivo_folios.close()


79
    contador = contador + 1


80
 #   f = open('c:\\registro\FoliosServicio.csv', 'r')


81
    n_folio = folio


82
    NuevoFolio()


83



84
    


85



86
def ConsultaServiciosFolio():


87
   


88
    print("*******CONSULTA DE SERVICIOS POR FOLIO********************")


89
    num_folio = (input("Teclee el numero de folio: "))


90
    import csv, operator


91
    with open('c:\\registro\FoliosServicio.csv') as csvarchivo:


92
        entrada = csv.reader(csvarchivo)


93
        sortedlist = sorted(entrada, key=operator.itemgetter(0), reverse=False)
#se ordenan los registros en funcion del folio

94
        print("Folio, 'Fecha, 'Cliente', 'Servicio', 'Costo', 'IVA', 'Total Servicio")


95
        for row in sortedlist:


96
            if row[0] == num_folio: #imprimir registro basado en rango de fechas
#se obtiene el valor especifico del folio del archivo según el folio deseado

97
                print (row)


98



99
    opcion = input("Teclea R para regresar al menu principal, S para salir del programa: ")


100
    if opcion=="R":


101
            Menu()


102
    elif opcion=="S":


103
        exit


104
    else:


105
        print("Intente de nuevo, tecle R o S")


106
       # Menu()


107



108



109
def ConsultaServiciosFecha():


110
   


111
    print("*****CONSULTA DE SERVICIOS POR FECHAS********************")


112
    fecha_inicial = (input("Teclee la fecha (dd/mm/aaaa): "))


113
    import csv, operator


114
    with open('c:\\registro\FoliosServicio.csv') as csvarchivo:


115
        entrada = csv.reader(csvarchivo)


116
        sortedlist = sorted(entrada, key=operator.itemgetter(0), reverse=False)


117
        print("Folio, 'Fecha, 'Cliente', 'Servicio', 'Costo', 'IVA', 'Total Servicio")


118
        for row in sortedlist:


119
            if row[1] == fecha_inicial: #imprimir registro basado en rango de fechas


120
                print (row)


121



122
    opcion = input("Teclea R para regresal al menu principal, S para salir del programa: ")


123
    if opcion=="R":


124
            Menu()


125
    elif opcion=="S":


126
        exit


127
    else:


128
        print("Intente de nuevo, tecle R o S")


129
       # Menu()


130



131
def ConsultaFolioEmp():


132
    print("*****CONSULTA DE SERVICIOS POR FECHAS********************")


133
    fecha_inicial = (input("Teclee la fecha inicial(dd/mm/aaaa): "))


134
    fecha_final = (input("Teclee la fecha final(dd/mm/aaaa): "))


135
    import csv, operator


136
    with open('c:\\registro\FoliosServicio.csv') as csvarchivo:


137
        entrada = csv.reader(csvarchivo)


138
        sortedlist = sorted(entrada, key=operator.itemgetter(0), reverse=False)


139
        print("Folio, 'Fecha, 'Cliente")


140
        for row in sortedlist:


141
            if row[1] >= fecha_inicial and row[1] <= fecha_final : #imprimir registro basado en rango de fechas


142
                print (row[0], row[1], row[2])


143



144
    opcion = input("Teclea R para regresal al menu principal, S para salir del programa: ")


145
    if opcion=="R":


146
            Menu()


147
    elif opcion=="S":


148
        exit


149
    else:


150
        print("Intente de nuevo, tecle R o S")


151



152
# main routine


153
contador = 1


154
n_folio = ""


155
Menu()

1
def Menu():


2
    print("Menu Principal")


3
    print("[1] Registro de Servicio")


4
    print("[2] Consulta de Folio por Numero")


5
    print("[3] Consulta de Servicios por Fecha")


6
    print("[4] Consulta de Folios por Fechas")


7
    print("[5] Salir")


8



9
    opcion = int(input("Elija una opción: "))


10
    if opcion==1:


11
        print("****************REGISTRO DE SERVICIO********************")        


12
        NuevoFolio()


13
    elif opcion ==2:


14
        ConsultaServiciosFolio()


15
    elif opcion ==3:


16
        ConsultaServiciosFecha()


17
    elif opcion==4:


18
        ConsultaFolioEmp()


19
    elif opcion==5:


20
        exit


21
    else:


22
        print("Intente de nuevo , seleccione 1-4")


23
        Menu()


24



25
def NuevoFolio():


26
    


27
    opcion = input("Desea agregar un equipo al folio(Y/N): ")


28
    if opcion=="Y":


29
        AgregarEquipo()


30
    elif opcion=="N":


31
        global n_folio


32
        print("Su numero de folio es: " + str(n_folio))


33
        exit


34
    else:


35
        print("Teclear Y para agregar folio, N para terminar folio")


36
        NuevoFolio()


37



38
def CreaNuevoFolio():


39
    import csv, operator


40
    with open('c:\\registro\FoliosServicio.csv') as csvarchivo:


41
        entrada = csv.reader(csvarchivo)


42
        sortedlist = sorted(entrada, key=operator.itemgetter(0), reverse=False)


43
        maxVal = []


44
        for row in sortedlist:


45
            maxVal.append(row[0])


46
    if contador == 1:


47
        siguiente = 1


48
        siguiente = siguiente + int(max(maxVal))


49
        return siguiente


50
    else:


51
        siguiente = 0


52
        siguiente = siguiente + int(max(maxVal))


53
        return siguiente


54



55
def AgregarEquipo():


56
    


57
    global contador


58
    global n_folio


59
    import csv, operator


60
    from datetime import datetime


61
    


62
    archivo_folios = open('c:\\registro\FoliosServicio.csv', 'a', newline='')


63



64
    folio = CreaNuevoFolio()


65
    


66
    fecha_folio = str(datetime.today().strftime('%Y-%m-%d'))


67
    nombre_cliente = input("Teclee el nombre del cliente: ")


68
    descripcion_servicio = input("Teclee el servicio a proporcionar: ")
#se preparan los datos para ser ligados en la estructura de datos

69
    descripcion_equipo = input("Teclee descripcion del equipo: ")


70
    costo_servicio = float(input("Teclee el costo del servicio: "))


71
    iva = float((costo_servicio * .16))


72
    precio_total=float((iva + costo_servicio))


73



74
    datos = [folio, fecha_folio, nombre_cliente, descripcion_servicio, descripcion_equipo, costo_servicio, iva, precio_total]
#se crea tupla con datos a guardar

75
    salida = csv.writer(archivo_folios)


76
    salida.writerow(datos)


77



78
    archivo_folios.close()


79
    contador = contador + 1


80
 #   f = open('c:\\registro\FoliosServicio.csv', 'r')


81
    n_folio = folio


82
    NuevoFolio()


83



84
    


85



86
def ConsultaServiciosFolio():


87
   


88
    print("*******CONSULTA DE SERVICIOS POR FOLIO********************")


89
    num_folio = (input("Teclee el numero de folio: "))


90
    import csv, operator


91
    with open('c:\\registro\FoliosServicio.csv') as csvarchivo:


92
        entrada = csv.reader(csvarchivo)


93
        sortedlist = sorted(entrada, key=operator.itemgetter(0), reverse=False)
#se ordenan los registros en funcion del folio

94
        print("Folio, 'Fecha, 'Cliente', 'Servicio', 'Costo', 'IVA', 'Total Servicio")


95
        for row in sortedlist:


96
            if row[0] == num_folio: #imprimir registro basado en rango de fechas
#se obtiene el valor especifico del folio del archivo según el folio deseado

97
                print (row)


98



99
    opcion = input("Teclea R para regresar al menu principal, S para salir del programa: ")


100
    if opcion=="R":


101
            Menu()


102
    elif opcion=="S":


103
        exit


104
    else:


105
        print("Intente de nuevo, tecle R o S")


106
       # Menu()


107



108



109
def ConsultaServiciosFecha():


110
   


111
    print("*****CONSULTA DE SERVICIOS POR FECHAS********************")


112
    fecha_inicial = (input("Teclee la fecha (dd/mm/aaaa): "))


113
    import csv, operator


114
    with open('c:\\registro\FoliosServicio.csv') as csvarchivo:


115
        entrada = csv.reader(csvarchivo)


116
        sortedlist = sorted(entrada, key=operator.itemgetter(0), reverse=False)


117
        print("Folio, 'Fecha, 'Cliente', 'Servicio', 'Costo', 'IVA', 'Total Servicio")


118
        for row in sortedlist:


119
            if row[1] == fecha_inicial: #imprimir registro basado en rango de fechas


120
                print (row)


121



122
    opcion = input("Teclea R para regresal al menu principal, S para salir del programa: ")


123
    if opcion=="R":


124
            Menu()


125
    elif opcion=="S":


126
        exit


127
    else:


128
        print("Intente de nuevo, tecle R o S")


129
       # Menu()


130



131
def ConsultaFolioEmp():


132
    print("*****CONSULTA DE SERVICIOS POR FECHAS********************")


133
    fecha_inicial = (input("Teclee la fecha inicial(dd/mm/aaaa): "))


134
    fecha_final = (input("Teclee la fecha final(dd/mm/aaaa): "))


135
    import csv, operator


136
    with open('c:\\registro\FoliosServicio.csv') as csvarchivo:


137
        entrada = csv.reader(csvarchivo)


138
        sortedlist = sorted(entrada, key=operator.itemgetter(0), reverse=False)


139
        print("Folio, 'Fecha, 'Cliente")


140
        for row in sortedlist:


141
            if row[1] >= fecha_inicial and row[1] <= fecha_final : #imprimir registro basado en rango de fechas


142
                print (row[0], row[1], row[2])


143



144
    opcion = input("Teclea R para regresal al menu principal, S para salir del programa: ")


145
    if opcion=="R":


146
            Menu()


147
    elif opcion=="S":


148
        exit


149
    else:


150
        print("Intente de nuevo, tecle R o S")


151



152
# main routine


153
contador = 1


154
n_folio = ""


155
Menu()


