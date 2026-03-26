---
title: "媒体控件"
post_status: publish
comment_status: open
taxonomy:
  category:
    - elementor-developers-docs
  post_tag:
    - Editor Controls
    - Src
    - Repos
---

# 媒体控件

<Badge type="tip" vertical="top" text="Elementor Core" /> <Badge type="warning" vertical="top" text="Basic" />

<img :src="$withBase('/assets/img/controls/control-media.png')" alt="Media Control" style="float: right;">

Elementor 媒体控件基于 WordPress 媒体库显示媒体选择器部分，允许用户从媒体库中选择图像。

该控件在继承 `Control_Base_Multiple` 类的 `Control_Media` 类中定义。

使用此控件时，应将 `type` 设置为 `\Elementor\Controls_Manager::MEDIA` 常量。

## 参数

<table>
	<thead>
		<tr>
			<th>名称</th>
			<th>类型</th>
			<th>默认值</th>
			<th>描述</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><code>type</code></td>
			<td><code>string</code></td>
			<td>media</td>
			<td>控件的类型。</td>
		</tr>
		<tr>
			<td><code>label</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>显示在字段上方的标签。</td>
		</tr>
		<tr>
			<td><code>description</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>显示在字段下方的描述。</td>
		</tr>
		<tr>
			<td><code>show_label</code></td>
			<td><code>bool</code></td>
			<td>true</td>
			<td>是否显示标签。</td>
		</tr>
		<tr>
			<td><code>label_block</code></td>
			<td><code>bool</code></td>
			<td>true</td>
			<td>是否在单独一行显示标签。</td>
		</tr>
		<tr>
			<td><code>separator</code></td>
			<td><code>string</code></td>
			<td>default</td>
			<td>设置控件分隔符的位置。可用值为 <code>default</code>、<code>before</code> 和 <code>after</code>。<code>default</code> 将隐藏分隔符，除非控件类型有特定的分隔符设置。<code>before</code> / <code>after</code> 会将分隔符定位在控件之前/之后。</td>
		</tr>
		<tr>
			<td><code>media_types</code></td>
			<td><code>array</code></td>
			<td>['image']</td>
			<td>支持的媒体类型。可用值为 <code>image</code>、<code>video</code>、<code>svg</code>、<code>application/pdf</code> 等。</td>
		</tr>
		<tr>
			<td><code>default</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>
				默认媒体值。
				<ul>
					<li><strong>$id</strong> (<code>int</code>) 媒体 ID。</li>
					<li><strong>$url</strong> (<code>string</code>) 媒体 URL。</li>
				</ul>
			</td>
		</tr>
	</tbody>
</table>

## Return Value

```
[
	'id' => '',
	'url' => '',
]
```

(_`array`_) An array containing image data:

* **$id** (_`int`_) Media id.
* **$url** (_`string`_) Media url.

## Usage

Add an image:

```php {14-23,36-37,39-40,42-47,52-69}
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'content_section',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'image',
			[
				'label' => esc_html__( 'Choose Image', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::MEDIA,
				'default' => [
					'url' => \Elementor\Utils::get_placeholder_image_src(),
				],
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();

		if ( empty( $settings['image']['url'] ) ) {
			return;
		}

		// Get image URL
		echo '<img src="' . $settings['image']['url'] . '">';

		// Get image 'thumbnail' by ID
		echo wp_get_attachment_image( $settings['image']['id'], 'thumbnail' );

		// Get image HTML
		$this->add_render_attribute( 'image', 'src', $settings['image']['url'] );
		$this->add_render_attribute( 'image', 'alt', \Elementor\Control_Media::get_image_alt( $settings['image'] ) );
		$this->add_render_attribute( 'image', 'title', \Elementor\Control_Media::get_image_title( $settings['image'] ) );
		$this->add_render_attribute( 'image', 'class', 'my-custom-class' );
		echo \Elementor\Group_Control_Image_Size::get_attachment_image_html( $settings, 'thumbnail', 'image' );
	}

	protected function content_template(): void {
		?>
		<#
		if ( '' === settings.image.url ) {
			return;
		}

		const image = {
			id: settings.image.id,
			url: settings.image.url,
			size: settings.image_size,
			dimension: settings.image_custom_dimension,
			model: view.getEditModel()
		};

		const image_url = elementor.imagesManager.getImageUrl( image );

		if ( '' === image_url ) {
			return;
		}
		#>
		<img src="{{ image_url }}">
		<?php
	}

}
```

Add a video media type to display a self hosted video:

```php
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'content_section',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'video',
			[
				'label' => esc_html__( 'Choose Video File', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::MEDIA,
				'media_types' => [ 'video' ],
				'default' => [
					'url' => \Elementor\Utils::get_placeholder_image_src(),
				],
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();
		$video_url = $settings['video']['url'];

if ( empty( $video_url ) ) {
			return;
		}
		?>
		<video src="<?php echo esc_attr( $video_url ); ?>" class="elementor-video"></video>
		<?php
	}

	protected function content_template(): void {
		?>
		<#
		const video_url = settings.video.url;

		if ( '' === video_url ) {
			return;
		}
		#>
		<video src="{{ video_url }}" class="elementor-video"></video>
		<?php
	}

}
```

Add a PDF file:

```php
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function register_controls(): void {

		$this->start_controls_section(
			'content_section',
			[
				'label' => esc_html__( 'Content', 'textdomain' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'pdf',
			[
				'label' => esc_html__( 'Choose PDF', 'textdomain' ),
				'type' => \Elementor\Controls_Manager::MEDIA,
				'media_types' => [ 'application/pdf' ],
			]
		);

		$this->end_controls_section();

	}

	protected function render(): void {
		$settings = $this->get_settings_for_display();
		$pdf_url = $settings['pdf']['url'];

		if ( ! empty( $pdf_url ) ) {
			return;
		}
		?>
		<a download href="<?php echo esc_attr( $pdf_url ); ?>">
			<?php echo esc_html__( 'Download PDF', 'textdomain' ); ?>
		</a>
		<?php
	}

	protected function content_template(): void {
		?>
		<#
		const pdf_url = settings.pdf.url;

		if ( '' === pdf_url ) {
			return;
		}
		#>
		<a download src="{{ pdf_url }}">
			<?php echo esc_html__( 'Download PDF', 'textdomain' ); ?>
		</a>
		<?php
	}

}
```