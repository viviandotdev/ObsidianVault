---

database-plugin: basic

---

```yaml:dbfolder
name: new database
description: new description
columns:
  __file__:
    key: __file__
    id: __file__
    input: markdown
    label: File
    accessorKey: __file__
    isMetadata: true
    skipPersist: false
    isDragDisabled: false
    csvCandidate: true
    width: 530
    position: 2
    isHidden: false
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
      wrap_content: true
      content_alignment: text-align-left
  Category:
    input: select
    accessorKey: Category
    key: Category
    id: Category
    label: Category
    position: 3
    skipPersist: false
    isHidden: true
    sortIndex: -1
    width: 139
    options:
      - { label: "Curated List", value: "Curated List", color: "hsl(164, 95%, 90%)"}
      - { label: "Learning", value: "Learning", color: "hsl(353, 95%, 90%)"}
      - { label: "Productivity", value: "Productivity", color: "hsl(18, 95%, 90%)"}
      - { label: "Finance", value: "Finance", color: "hsl(216, 95%, 90%)"}
      - { label: "Focus", value: "Focus", color: "hsl(67, 95%, 90%)"}
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: false
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  Status:
    input: select
    accessorKey: Status
    key: Status
    id: Status
    label: Status
    position: 1
    skipPersist: false
    isHidden: false
    sortIndex: -1
    width: 98
    options:
      - { label: "idea", value: "idea", color: "hsl(214,72%,64%)"}
      - { label: "completed", value: "completed", color: "hsl(152, 95%, 90%)"}
      - { label: "hold", value: "hold", color: "hsl(273, 95%, 90%)"}
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: false
      task_hide_completed: true
      footer_type: none
      persist_changes: false
      option_source: manual
  modified:
    input: calendar_time
    accessorKey: modified
    key: modified
    id: modified
    label: modified
    position: 4
    skipPersist: false
    isHidden: true
    sortIndex: -1
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: false
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  created:
    input: text
    accessorKey: created
    key: created
    id: created
    label: created
    position: 5
    skipPersist: false
    isHidden: true
    sortIndex: -1
    width: 182
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: false
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  tags:
    input: text
    accessorKey: tags
    key: tags
    id: tags
    label: tags
    position: 6
    skipPersist: false
    isHidden: false
    sortIndex: -1
    width: 180
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: false
      task_hide_completed: true
      footer_type: none
      persist_changes: false
      content_alignment: text-align-left
config:
  remove_field_when_delete_column: false
  cell_size: normal
  sticky_first_column: false
  group_folder_column: 
  remove_empty_folders: false
  automatically_group_files: false
  hoist_files_with_empty_attributes: true
  show_metadata_created: false
  show_metadata_modified: false
  show_metadata_tasks: false
  show_metadata_inlinks: false
  show_metadata_outlinks: false
  show_metadata_tags: false
  source_data: query
  source_form_result: "FROM \"40 Spaces/Efforts/Life Optimization Content\""
  source_destination_path: 40 Spaces/Efforts/Systems for Life
  row_templates_folder: 10 Extras/Templates
  current_row_template: 10 Extras/Templates/idea.systems-for-life.md
  pagination_size: 10
  font_size: 16
  enable_js_formulas: false
  formula_folder_path: /
  inline_default: false
  inline_new_position: last_field
  date_format: yyyy-MM-dd
  datetime_format: "yyyy-MM-dd HH:mm:ss"
  metadata_date_format: "yyyy-MM-dd HH:mm:ss"
  enable_footer: false
  implementation: default
filters:
  enabled: true
  conditions:
      - condition: AND
        disabled: false
        label: "ideas"
        color: "hsl(184, 95%, 90%)"
        filters:
        - field: Status
          operator: EQUAL
          value: "idea"
          type: select
```