PROJECT := pcb

.PHONY: erc
erc:
	kicad-cli sch erc $(PROJECT).kicad_sch

.PHONY: drc
drc:
	kicad-cli pcb drc $(PROJECT).kicad_pcb

.PHONY: export-gerbers
export-gerbers:
	# create backup
	if [ -d gerbers ]; then mv gerbers gerbers_$(shell date +"%Y-%m-%d_%H:%M:%S"); fi
	mkdir -p gerbers
	kicad-cli pcb export gerbers --board-plot-params -o gerbers $(PROJECT).kicad_pcb
	kicad-cli pcb export drill --excellon-separate-th --generate-map --map-format gerberx2 -o gerbers $(PROJECT).kicad_pcb
	rm $(PROJECT)_gerbers.zip || true
	zip -r $(PROJECT)_gerbers.zip gerbers

.PHONY: clean
clean:
	rm -rf gerbers
	rm $(PROJECT)_gerbers.zip
