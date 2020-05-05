.PHONY: clean 4klang.o

.DEFAULT_GOAL := 4klangrender

4klang.asm: ../4klang.asm
	cp ../4klang.asm .

4klang.inc: ../4klang.inc
	sed -e 's/\;\%define SINGLE_TICK_RENDERING/\%define SINGLE_TICK_RENDERING/;s/\;\%define AUTHORING/\%define AUTHORING/' ../4klang.inc > 4klang.inc

4klang.o: 4klang.asm 4klang.inc
	yasm -f elf64 -o "$@" "$<"

4klangrender: 4klang.o 4klangrender.c
	tcc 4klangrender.c 4klang.o -o "$@"

run: 4klangrender
	./4klangrender | sox -t raw -b 32 -e float -r 44100 -c 2 - -d

clean:
	rm -f 4klang.o 4klang.asm 4klang.inc
