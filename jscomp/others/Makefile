include ../Makefile.shared

COMPILER=../bin/bsc.exe

MAP_FILES= node bs

SOURCE_LIST= node_path node_fs node_process dict node_module js_array js_string \
	js_re js_null_undefined node_buffer js_types js_json js_obj \
	bs_dyn bs_dyn_lib bs_vector bs_list bs_option bs_result \
	node_child_process js_boolean js_math js_dict js_date js_global js_cast js_promise dom

$(addsuffix .cmj, $(SOURCE_LIST)): $(addsuffix .cmj, $(MAP_FILES))

RUNTIME := $(addsuffix .cmj, $(SOURCE_LIST)) $(addsuffix .cmi, $(SOURCE_LIST))

BS_COMMON_FLAGS= -no-alias-deps -bs-no-version-header -absname -bs-diagnose -bs-no-check-div-by-zero -bs-cross-module-opt -bs-package-name bs-platform


BS_FLAGS=  $(BS_COMMON_FLAGS) $(BS_PKG_FLAGS)

COMPFLAGS += $(BS_FLAGS)  -I ../runtime -I ../stdlib -w +3-40-49 -warn-error A -bin-annot


node.cmi : $(COMPILER)
node.cmj : $(COMPILER)
bs.cmi : $(COMPILER)
bs.cmj : $(COMPILER)
$(RUNTIME): $(COMPILER)

all: $(RUNTIME)

clean::
	rm -f *.cm*
	rm -f *~
	rm -f  *.annot
	rm -f *.rawlambda *.lam *.lambda *.map


.mli.cmi:
	$(COMPILER) $(INCLUDES) $(COMPFLAGS)  -c $<
.ml.cmj:
	$(COMPILER) $(INCLUDES) $(COMPFLAGS)  -c $<


-include .depend

ML_SOURCES=$(addsuffix .ml, $(SOURCE_LIST))
MLI_SOURCES=$(addsuffix .mli, $(SOURCE_LIST))

depend:
	$(CAMLDEP) -native $(INCLUDES) $(ML_SOURCES) $(MLI_SOURCES) | sed -e 's/\.cmx/.cmj/g' >.depend
