GENERATED_FILES: output/texas.csv

.PHONY: all cleanup

all: $(GENERATED_FILES)

include ../../../Makefile

output/texas.csv: \
		input/Copy_of_RESULTS_-_MEDIA_REQUEST_-_January_1_2010_to_Jul_14_2022.xlsx \
		$(SHARED_DIR)/src/normalize_data.py \
		src/fix_mismatched_awarded.py \
		src/dedupe.py
	in2csv $< --no-inference | \
	python src/fix_mismatched_awarded.py | \
	csvgrep -c AWARDED -r YES | \
	csvgrep -i -c FK_VCMPLNT_STSCD -r 975 | \
	python src/dedupe.py | \
	python $(SHARED_DIR)/src/normalize_data.py Texas \
		--employer_name OWNER_CORP_NM \
		--employer_dba_name DBA_NM \
		--date_opened FILG_DT \
		--date_closed STS_DT \
	> $@

cleanup:
	rm -f output/*