# Custom Inputを試す
- [simple_form 公式のwiki参考](https://github.com/plataformatec/simple_form/wiki/Custom-inputs-examples)

```ruby
# app/inputs/append_text_input.rb
class AppendTextInput < SimpleForm::Inputs::StringInput
  def input(wrapper_options = nil)
    input_html_classes.push('test_custom')
    if options[:append]
      return template.content_tag(:div, class: 'input-group') do
        template.concat super(wrapper_options)
        template.concat content_tag(:span, options[:append], class: 'input-group-text')
      end
    end
    super(wrapper_options)
  end
end
```

```haml
-#app/views/articles/_form.html.haml
= f.input :title, as: :append_text, input_html: {type: 'text'}, append: '様'
```
