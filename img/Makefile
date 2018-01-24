SRCS = $(wildcard *.txt)
OBJS = $(patsubst %.txt,%.svg,$(SRCS))

all: $(OBJS)

%.svg: %.txt
	gitink --in-file=$< --time-direction=0 --scale=1.0 > $@

clean: 
	rm *.svg
