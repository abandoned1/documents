Sass 用法
1. 安装指南
	http://www.w3cplus.com/sassguide/install.html
2. manual:
	http://sass-lang.com/documentation/file.SASS_REFERENCE.html
3. 自动编译指令
	cd themes/xunyun/
	compass watch bag


================ 以下是less和scss的一些区别 =================

1. @import
2.  less: main.less/_main.
	scss || @import main;
3. scss:
	$color: #BADA55;
   less:
	@color: #BADA55;
4. Mixins:
	sass: @mixin bordered()
	less: .bordered()
5. sass:
	@mixin box-shadow($shadows...) {
		-moz-box-shadow: $shadows;
		-webkit-box-shadow: $shadows;
		box-shadow: $shadows;
	}
	.shadows {
		@include box-shadow(0 4px 5px #666, 2px 6px 10px #999);
	}

   less:
	.box-shadow(@shadows...) {
		-moz-box-shadow: @shadows;
		-webkit-box-shadow: @shadows;
		box-shadow: @shadows;
	}
	.shadows {
		.box-shadow(~"0 4px 5px #666, 2px 6px 10px #999");
	}
6. Operations:
	.container {
		width: 300px + 2em // == 302 px o_0
	}
7. Variables:
	@base-font-size: 16;
	@base-spacing-unit: 24;
	html{
		font-size: (@base-font-size/16) * 1em;
		margin-bottom: @base-spacing-unit*1px;
	}
8. functions:
	sass: http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html
	less: http://lesscss.org/#reference
9. Interpolation:
	sass:
		$base-url: "../images";
		.container {
			background-image: url("#{$base-url}/bg.png");
		}
	less:
		@base-url: "../images";
		.container {
			background-images: url("@{base-url}/bg.png");
		}
	The only difference is the syntax: #{ $var } with sass and @{ var } with less.
10. loops:
	sass:
		$index: 5;

		@while $index > 0 {
			// Interpolate the class name
			.container-#{$index} {
				z-index: $index;
			}
			// Decrease the index
			$index: $index-1;
		}

	less:
		.loop (@index) when (@index > 0) {
			// Interpolate the class name
			.container-@{index} {
				z-index: @index;
			}
			// Declare the index and start the loop again
			.loop (@index - 1);
		}

		// Stop the loop at 0
		.loop (0) {}

		// Start the loop
		.loop(5);

11. Extend:
	sass:
		.error {
			border: 1px #f00;
			background-color: #fdd;
		}

		.serious-error {
			@extend .error;
			border-width: 3px;
		}

		======================output as below code ====================
		.error, .serious-error {
			border: 1px #f00;
			background-color: #fdd;
		}

		.serious-error {
			border-width: 3px;
		}

		sass silent classes:
			a%error {
				color: red;
				font-weight: bold;
			}

			.notice {
				@extend %error;
			}

			==============output as below code ==========
			a.notice {
				color: red;
				font-weight: bold;
			}

		less silent classes:
			.error() {
				a& {
					color: red;
					font-weight: bold;
				}
			}

			.notice {
				.error();
			}
		less v1.4
			.error {
				border: 1px #f00;
				background-color: #fdd;
			}

			.serious-error:extend(.error) {
				border-width: 3px;
			}

12. !default variables
13. @content
	sass:
		@mixin apply-to-ie-only {
			*html {
				@content;
			}
		}

		@include apply-to-ie6-only {
			#logo {
				background-image: url(/logo.gif);
			}
		}
	================output as below code =====================
	*html #logo {
		background-image: url(/logo.gif);
	}

	less: =============similar as sass function as above ===========
		@mixin border-badass($side) {
			border-#{$side}: 1px #BADA55 solid;
		}
		.container {
			@include border-badass(left);
		}

		============output as below code =================
		.container {
			border-left: 1px #BADA55 solid;
		}




