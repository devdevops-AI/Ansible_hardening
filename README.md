# Ansible_hardening

This repository contains an Ansible playbook for system hardening. A Jinja2 template located at `templates/report.html.j2` generates an HTML compliance report. The template expects a list variable named `location_reports` with one entry per site. Each entry should contain:

- `name` – the location name (e.g. "A", "B", etc.)
- `compliant` – number of compliant checks in that location
- `non_compliant` – number of failed checks in that location
- `compliant_items` – list of compliant setting names
- `non_compliant_items` – list of non-compliant setting names

The template automatically totals all locations for the summary tab and displays a separate tab for each location.

