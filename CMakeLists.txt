cmake_minimum_required(VERSION 3.24)
project(Proyecto1)

set(CMAKE_CXX_STANDARD 20)

# Diana, si estás viendo esto, aquí están las instrucciones de cómo poner SDL2 en CLion con CMake.
# Lo estoy haciendo en mi máquina de escritorio Windows así que te debería funcionar.
# 1. Descargar SDL2 en el sitio oficial. Ponerlo en cualquier lugar, yo lo puse en un folder lib fuera del proyecto,
#    pero en realidad no importa
# 2. Vas a tener que crear un nuevo perfil de Cmake para agregarle un par de variables de entorno. Podés agregárselas al
#    sistema entero y saltarte esto, pero considero que es una hueva así que lo hago de esta manera:
#        2.1 Te vas a Settings >> Build, Execution, Deployment >> CMake y creas una copia del perfil default. Por ahora,
#            vas a tener que deshabilitar el perfil default dándole clic al checkbox que sale.
#        2.2 En la parte de environments le vas a agregar esto:
#                SDL2_DIR=...\libs\SDL2-2.26.3
#             o alternativamente:
#                CMAKE_PREFIX_PATH=...\libs
#
# 3. sdl básicamente te pone automáticamente un wrapper para el main. Entonces, tu main está obligado a tener como
#    parámetros argc y argv. Si no los tenés, te va a tirar errores bieeen raros.
# 4. Por default, sdl también va a requerir un runtime library. La manera más paja es solo meter la runtime library en
#    el folder ese que te genera el cmake para el output xd. Básicamente copia el archivo de
#    SDL2-2.26.3\x86_64-w64-mingw32\bin\SDL.dll y lo ponés en cmake-debug-blah-blah-blah.
#    Técnicamente podrías hacer un script para automatizar esto pero que hueva xd

# INFORMACIÓN IMPORTANTE
# Por default, sdl en windows redirige stdout y stderr hacia null (básicamente ignora los prints). Así que tenemos que
# usar logging.
find_package(SDL2 REQUIRED)
find_package(OpenMP REQUIRED)
link_libraries(OpenMP::OpenMP_CXX)

add_executable(Proyecto1 main.cpp)
target_link_libraries(Proyecto1 SDL2::SDL2main SDL2::SDL2)
