GENERATED_FILES: output/massachusetts.csv

.PHONY: all cleanup

.INTERMEDIATE: output/pre_cleaned.csv

all: $(GENERATED_FILES)

include ../../../Makefile

output/massachusetts.csv: \
		output/pre_cleaned.csv \
		$(SHARED_DIR)/src/normalize_data.py \
		hand/converters_violation_category.yaml
	cat $< | python $(SHARED_DIR)/src/normalize_data.py Massachusetts \
		--explode-violations \
		--violations-delim "," \
		--employer_name Employer \
		--employer_dba_name DBA \
		--employer_city city \
		--violation_category "Violation Description" \
		--date_opened "Date Issued" \
		--amount_assessed "Total Assessed" \
		--paid-in-full "Paid In Full" \
		> $@

# make massachusetts-specific changes to the data
output/pre_cleaned.csv: \
		src/clean.py \
		input/Data_Portal_Citations.xlsx
	python $^ > $@

cleanup:
	rm -f output/*