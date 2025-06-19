# Ansible_hardening

This repository contains an Ansible playbook for system hardening. A Jinja2 template located at `templates/report.html.j2` generates an HTML compliance report. The template expects a list variable named `location_reports` with one entry per site. Each entry should contain:

- `name` – the location name (e.g. "A", "B", etc.)
- `compliant` – number of compliant checks in that location
- `non_compliant` – number of failed checks in that location
- `compliant_items` – list of compliant setting names
- `non_compliant_items` – list of non-compliant setting names

The template automatically totals all locations for the summary tab and displays a separate tab for each location. Each table also shows compliance percentages.

After running the playbook you can generate the HTML report by providing
`location_reports` data. A small example (`locations.yml`) might look like:

```yaml
location_reports:
  - name: A
    compliant: 10
    non_compliant: 5
    compliant_items:
      - ctrl1
      - ctrl2
    non_compliant_items:
      - ctrl3
```

The repository includes a simple `inventory.ini` with placeholder hosts for
four locations. Run the playbook against that inventory and provide the
`location_reports` data to render an HTML report:

```bash
ansible-playbook -i inventory.ini hardening.yml -e @locations.yml
```

When finished, the template task at the end of the playbook writes
`compliance_report.html`. A sample of the rendered output can be found in
`sample_report.html` for reference.


