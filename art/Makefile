# ============================================================
# 🖼️  ASCII Art → SVG Converter
#     Requires: aasvg (https://github.com/mbndr/aasvg)
# ============================================================

# Detect aasvg binary
AASVG := $(shell which aasvg)

# Error if aasvg is missing
ifeq ($(AASVG),)
	$(error aasvg (ASCII art to SVG converter) not found. To install: 'go install github.com/mbndr/aasvg@latest')
endif

# ------------------------------------------------------------
# 🧩 Variables
# ------------------------------------------------------------
# Input and output directories (customize if needed)
SRC_DIR := .
OUT_DIR := .

# Pattern for ASCII files
ASCII_FILES := $(wildcard $(SRC_DIR)/*.txt $(SRC_DIR)/*.asc $(SRC_DIR)/*.ascii)
SVG_FILES := $(patsubst $(SRC_DIR)/%.txt,$(OUT_DIR)/%.svg,$(filter %.txt,$(ASCII_FILES))) \
			$(patsubst $(SRC_DIR)/%.asc,$(OUT_DIR)/%.svg,$(filter %.asc,$(ASCII_FILES))) \
			$(patsubst $(SRC_DIR)/%.ascii,$(OUT_DIR)/%.svg,$(filter %.ascii,$(ASCII_FILES)))

# ------------------------------------------------------------
# 🎨 Rules
# ------------------------------------------------------------

# Default target: convert all ASCII files to SVG
all: $(SVG_FILES)
	@echo "✅ All SVGs generated successfully!"

# 🎨 Conversion rule: .txt, .asc, or .ascii → .svg
$(OUT_DIR)/%.svg: $(SRC_DIR)/%.txt
	@echo "🎨 Converting $< → $@"
	@$(AASVG) < $< > $@

$(OUT_DIR)/%.svg: $(SRC_DIR)/%.asc
	@echo "🎨 Converting $< → $@"
	@$(AASVG) < $< > $@

$(OUT_DIR)/%.svg: $(SRC_DIR)/%.ascii
	@echo "🎨 Converting $< → $@"
	@$(AASVG) < $< > $@

# ------------------------------------------------------------
# 🧹 Utility targets
# ------------------------------------------------------------

# Remove generated SVG files
clean:
	@echo "🧹 Removing generated SVG files..."
	@rm -f $(SVG_FILES)

# Print debug info
info:
	@echo "AASVG: $(AASVG)"
	@echo "SRC_DIR: $(SRC_DIR)"
	@echo "OUT_DIR: $(OUT_DIR)"
	@echo "ASCII_FILES: $(ASCII_FILES)"
	@echo "SVG_FILES: $(SVG_FILES)"

.PHONY: all clean info

