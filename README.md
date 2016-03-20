Packages needed:

	perl-DateTime
	liberation-sans-fonts
	gnuplot
	bc

To setup:

	cp bin/copy-to-website.example bin/copy-to-website
	# edit bin/copy-to-website to copy the files to your website
	cp titles.example titles
	# edit titles to have the IPs and hostnames of your remote clocks
	cp -a runX run1
	# edit run1/index.html.tmpl to show the graphs for the IPs of the remote clocks
	# edit bin/run if your logdir is different: LOGDIR=/var/log/chrony

To run (under screen/tmux):

	cd run1 ; ../bin/loop
	# edit run1/notes to keep notes

Optional scripts:
	run1/startime - echo the unix timestamp to start at
	run1/custom-plot - generate some custom plots
