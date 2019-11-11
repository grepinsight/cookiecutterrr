PREFIX ?= /usr/local/bin

install: doc
	R CMD INSTALL .
	make test
develop:
	tmux split-window -v -c "#{pane_current_path}" 'R' && \
	tmux send-keys "setwd(Sys.getenv('PWD')); devtools::load_all('.')" Enter
doc:
	rm -rf NAMESPACE
	Rscript -e "setwd(Sys.getenv('PWD')); devtools::document(roclets = c('rd', 'collate', 'namespace'))"
test:
	Rscript -e "setwd(Sys.getenv('PWD')); devtools::load_all(); devtools::test()"
test-continuous:
	find R/ tests/testthat/ -type f -name "*.R" | entr make test
pkgdown:
	Rscript -e 'pkgdown::build_site()'
	open docs/index.html
