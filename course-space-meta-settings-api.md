## Settings API for Course/Space Meta

If you want to add your custom meta fields to the Course/Space settings, you can use the Settings API provided by FluentCommunity. This allows you to create custom settings sections and fields that can be used to store additional information related to your courses or spaces.


```php

/**
* Example: Add a custom meta box to the Course and Space settings
 * We are intruducing the new fluent_community/on_wp_init hook so you don't need to check the plugin version to use the Settings API.
 * It's fully compatible with the previous versions of the plugin.
 */
add_action('fluent_community/on_wp_init', function ($app) {
    $api = \FluentCommunity\App\Functions\Utility::extender();
    $api->addMetaBox('my_metabox_example', [
        'section_title'   => 'My Custom Course / Space Meta Example ', // title of your meta settings
        'fields_callback' => function ($spaceOrCourse) {
            // Available fields for Course or Space settings
            return [
                'text_field'    => [
                    'label'       => 'Text Field',
                    'data_type'   => 'text', // or number, email, password, textarea etc
                    'type'        => 'text',
                    'help_text'   => 'This is my example text field',
                    'placeholder' => 'Enter some text here',
                ],
                'radio_group'   => [
                    'label'     => 'Radio Group',
                    'type'      => 'radio',
                    'help_text' => 'This is my example radio group',
                    'options'   => [
                        [
                            'label' => 'Option 1',
                            'value' => 'option_1'
                        ],
                        [
                            'label' => 'Option 2',
                            'value' => 'option_2'
                        ]
                    ]
                ],
                'checkboxes'    => [
                    'label'     => 'Checkboxes',
                    'type'      => 'checkbox',
                    'help_text' => 'This is my example checkbox group',
                    'options'   => [
                        [
                            'label' => 'Check 1',
                            'value' => 'check_1'
                        ],
                        [
                            'label' => 'Check 2',
                            'value' => 'check_2'
                        ]
                    ]
                ],
                'date'          => [
                    'label'       => 'Date Picker',
                    'type'        => 'date',
                    'help_text'   => 'This is my example date picker',
                    'placeholder' => 'Select a date',
                ],
                'color_picker'  => [
                    'label'       => 'Color Picker',
                    'type'        => 'color_picker',
                    'help_text'   => 'This is my example color picker',
                    'placeholder' => 'Select a color',
                ],
                'raw_hrml'      => [
                    'label'   => '',
                    'type'    => 'raw_html',
                    'content' => '<p>This is a raw HTML field. You can add any HTML content here.</p>',
                ],
                'multi_selects' => [
                    'label'       => 'Select Boxes',
                    'type'        => 'select',
                    'is_multiple' => true,
                    'help_text'   => 'This is my example select box',
                    'options'     => [
                        [
                            'label' => 'Hello 1',
                            'value' => 'value_1'
                        ],
                        [
                            'label' => 'Hello 2',
                            'value' => 'value_2'
                        ]
                    ],
                    'placeholder' => 'Select Some Options',
                ],
                'checkbox'      => [
                    'true_value'     => 'yes',
                    'false_value'    => 'no',
                    'type'           => 'inline_checkbox',
                    'checkbox_label' => 'This is my inline checkbox label',
                ]
            ];
        },
        'data_callback'   => function ($spaceOrCourse) {
            // You can use this callback to retrieve the saved settings for the Course or Space
            // You can use the default meta data api to get the settings or use your own data retrieval logic
            // $spaceOrCourse is a \FluentCommunity\App\Models\Space or \FluentCommunity\App\Models\Course object
            $settings = $spaceOrCourse->getCustomMeta('_my_metabox_example_settings', []);
            $defaults = [
                'text_field'    => '',
                'radio_group'   => '',
                'checkboxes'    => [],
                'date'          => '',
                'date_time'     => '',
                'color_picker'  => '',
                'multi_selects' => [],
                'checkbox'      => 'no'
            ];
            $settings = wp_parse_args($settings, $defaults);
            
            // You must have to return the settings array with the keys matching the field names defined in the fields_callback
            return $settings;
        },
        'save_callback'   => function ($settings, $spaceOrCourse) {
            if (!is_array($settings)) {
                return;
            }
            
            // You can use this callback to save the settings for the Course or Space.
            // You can use the default meta data api to save the settings or use your own data saving logic
            // Please make sure to validate and santize the settings before saving them
  
            $spaceOrCourse->updateCustomMeta('_my_metabox_example_settings', $settings);
        }
    ], ['course', 'space']); // You can specify the types of objects where this meta box should appear. In this case, it will appear in both Course and Space settings.
});
```
