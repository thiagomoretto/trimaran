
MAKEFILE = $(ELCOR_HOME)/mdes/Makefile

#
# Specify the path of the HMDES2->LMDES2 compiler
#
HC = $(IMPACT_REL_PATH)/scripts/hc

STD_MDES = \
hpl_pd_elcor_std.hmdes2

MDES_INCLUDES = structure_pristine.hmdes2 
HPL_PD_INCLUDES = \
hpl_pd_ops.hmdes2 \
hpl_pd_pristine.hmdes2 \
hpl_pd_elcor.hmdes2

LOOP_ACC_FILES = \
loop_acc/loop_elcor_std.hmdes2 \
loop_acc/loop_pristine.hmdes2 \
loop_acc/loop_elcor.hmdes2 \
loop_acc/loop_ops.hmdes2 \
loop_acc/loop_acc.hmdes2

ARM_FILES = \
arm/arm_elcor_std.hmdes2 \
arm/arm_pristine.hmdes2 \
arm/arm_elcor.hmdes2 \
arm/arm_custom_ops.hmdes2 \
arm/arm_ops.hmdes2

all: std_mdes
 
std_mdes : $(STD_MDES:.hmdes2=.lmdes2)

$(STD_MDES:.hmdes2=.lmdes2) : %.lmdes2 : %.hmdes2 $(MDES_INCLUDES) $(HPL_PD_INCLUDES)
	@echo '*** Processing Mdes $< ***'
	$(HC) $<
	rm -rf $*.hmdes2pp
	@echo '*** Done'

arm : arm/arm_elcor_std.lmdes2

arm/arm_elcor_std.lmdes2 : $(ARM_FILES) $(MDES_INCLUDES)
	(cd arm; $(MAKE))

loop_acc : loop_acc/loop_elcor_std.lmdes2
     
loop_acc/loop_elcor_std.lmdes2 : $(LOOP_ACC_FILES) $(MDES_INCLUDES)
	(cd loop_acc; $(MAKE)) 
        
clean:
	rm -rf core *.hmdes2pp *.lmdes2 *~
	rm -rf arm/*.hmdes2pp arm/*.lmdes2 arm/*~
	rm -rf loop_acc/*.hmdes2pp loop_acc/*.lmdes2 loop_acc/*~

%.lmdes2 : %.hmdes2
	@echo '*** Mdes $< ***'
	$(HC) $<
