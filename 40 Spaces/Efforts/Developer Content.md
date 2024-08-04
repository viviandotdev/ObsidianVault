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
    position: 2
    isHidden: false
    sortIndex: -1
    width: 440
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: true
      task_hide_completed: true
      footer_type: none
      persist_changes: false
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
    width: 188
    isSorted: false
    isSortedDesc: false
    options:
      - { label: "system-design", value: "system-design", color: "hsl(346, 95%, 90%)"}
      - { label: "react", value: "react", color: "hsl(73, 95%, 90%)"}
      - { label: "leetcode", value: "leetcode", color: "hsl(127, 95%, 90%)"}
    config:
      enable_media_view: true
      link_alias_enabled: true
      media_width: 100
      media_height: 100
      isInline: false
      task_hide_completed: true
      footer_type: none
      persist_changes: false
  modified:
    input: text
    accessorKey: modified
    key: modified
    id: modified
    label: modified
    position: 100
    skipPersist: false
    isHidden: true
    sortIndex: -1
    width: 316
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
    position: 100
    skipPersist: false
    isHidden: false
    sortIndex: -1
    width: 255
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
      wrap_content: true
  status:
    input: select
    accessorKey: status
    key: status
    id: Status
    label: status
    position: 1
    skipPersist: false
    isHidden: false
    sortIndex: 1
    width: 120
    isSorted: true
    isSortedDesc: false
    options:
      - { label: "idea", value: "idea", color: "hsl(292, 95%, 90%)"}
      - { label: "completed", value: "completed", color: "hsl(255, 95%, 90%)"}
      - { label: "hold", value: "hold", color: "hsl(189, 95%, 90%)"}
      - { label: "#🟩", value: "#🟩", color: "hsl(244, 95%, 90%)"}
      - { label: "in-progress", value: "in-progress", color: "hsl(94, 95%, 90%)"}
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
  source_form_result: "FROM \"40 Spaces/Efforts/Developer Content\""
  source_destination_path: /
  row_templates_folder: 10 Extras/Templates
  current_row_template: 
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
        disabled: true
        label: "ideas"
        color: "hsl(87, 95%, 90%)"
        filters:
        - field: status
          operator: EQUAL
          value: "idea"
          type: select
      - condition: AND
        disabled: true
        label: "in-progress"
        color: "hsl(157, 95%, 90%)"
        filters:
        - field: status
          operator: EQUAL
          value: "in-progress"
          type: select
```