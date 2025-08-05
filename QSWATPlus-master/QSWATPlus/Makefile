###############################################################################
# QSWATPlus Makefile - Adaptado para Python 3.12 y 3.9
###############################################################################

QSWAT_PROJECT = QSWATPlus
COMPILER = C:/PROGRA~2/MICROS~2/2022/BUILDT~1/VC/Tools/MSVC/14.44.35207/bin/Hostx64/x64/cl.exe

# SDK de Windows (rutas en formato 8.3 para evitar problemas con espacios)
WINSDK_INCLUDE = \
	C:/PROGRA~2/WINDOW~2/10/Include/10.0.22621.0/ucrt \
	C:/PROGRA~2/WINDOW~2/10/Include/10.0.22621.0/shared \
	C:/PROGRA~2/WINDOW~2/10/Include/10.0.22621.0/um

###############################################################################
# Targets
###############################################################################

QSWATPlus3_9:
	$(MAKE) QSWAT_PROJECT=QSWATPlus \
		PYTHON_INCLUDE="C:/OSGeo4W/apps/Python39/include" \
		PYTHON_LIB="C:/OSGeo4W/apps/Python39/libs" \
		PYTHON_EXE="C:/OSGeo4W/bin/python3.exe" \
		CYTHON="C:/OSGeo4W/bin/python3.exe -m cython" \
		build

QSWATPlus3_12:
	$(MAKE) QSWAT_PROJECT=QSWATPlus \
		PYTHON_INCLUDE="C:/OSGeo4W/apps/Python312/include C:/OSGeo4W/apps/Python312/Lib/site-packages/numpy/core/include" \
		PYTHON_LIB="C:/OSGeo4W/apps/Python312/libs" \
		PYTHON_EXE="C:/OSGeo4W/bin/python3.exe" \
		CYTHON="C:/OSGeo4W/bin/python3.exe -m cython" \
		build

###############################################################################
# Build rules
###############################################################################

build:
	@echo "Compilando $(QSWAT_PROJECT) usando Python en $(PYTHON_EXE)"
	@echo "Incluyendo: $(PYTHON_INCLUDE)"
	@echo "Librería: $(PYTHON_LIB)"
	$(CYTHON) --fast-fail --cplus -3 -o jenks.c jenks.pyx
	$(CYTHON) --fast-fail --cplus -3 -o dataInC.c dataInC.pyx
	$(CYTHON) --fast-fail --cplus -3 -o polygonizeInC.c polygonizeInC.pyx
	$(COMPILER) /nologo /O2 /EHsc /LD /TP \
		$(foreach inc,$(PYTHON_INCLUDE),/I$(inc)) \
		$(foreach inc,$(WINSDK_INCLUDE),/I$(inc)) \
		jenks.c /link /OUT:jenks.pyd /LIBPATH:$(PYTHON_LIB)
	$(COMPILER) /nologo /O2 /EHsc /LD /TP \
		$(foreach inc,$(PYTHON_INCLUDE),/I$(inc)) \
		$(foreach inc,$(WINSDK_INCLUDE),/I$(inc)) \
		dataInC.c /link /OUT:dataInC.pyd /LIBPATH:$(PYTHON_LIB)
	$(COMPILER) /nologo /O2 /EHsc /LD /TP \
		$(foreach inc,$(PYTHON_INCLUDE),/I$(inc)) \
		$(foreach inc,$(WINSDK_INCLUDE),/I$(inc)) \
		polygonizeInC.c /link /OUT:polygonizeInC.pyd /LIBPATH:$(PYTHON_LIB)

###############################################################################
# Clean rule
###############################################################################

clean:
	@echo "Limpiando archivos generados..."
	-del /Q jenks.c dataInC.c polygonizeInC.c
	-del /Q jenks.pyd dataInC.pyd polygonizeInC.pyd
	-del /Q *.obj *.pdb

###############################################################################
# Default target
###############################################################################

all: QSWATPlus3_12
