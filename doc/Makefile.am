# Copyright 2017 Artem Savkov <artem.savkov@gmail.com>
# Copyright 2017 Alex Schroeder <alex@gnu.org>
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

EXTRA_DIST = mastodon-help.txt

install-data-local:
	if [ -f $(datadir)/help.txt ]; then \
		for file in $(EXTRA_DIST); do \
		  mkdir -p $(DESTDIR)$(datadir); \
			$(INSTALL) -m 644 $(srcdir)/$$file $(DESTDIR)$(datadir)/; \
		done \
	else \
		echo "Detected dir $(datadir) is not bitlbee's data dir"; \
		echo "Skipping help install"; \
	fi

HELP.md: mastodon-help.txt
	sed \
	-e '1i# Bitlbee Mastodon\nThis document was generated from the help text for the plugin.\n' \
	-e '1d' \
	-e 's/^%$$//g' \
	-e 's/^\?m/## /g' \
	-e 's/^\?/## /g' \
	-e 's//*/g' \
	-e 's/^ \*/* */g' \
	-e 's/\*help m\([a-z]*2*\)\*/[\1](#\1)/g' \
	-e 's/^\(\*[^ ].*\)/\1  /g' \
	< $^ > $@
