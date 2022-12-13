import 'intl-tel-input/build/css/intlTelInput.css';
import { requestIdleCallback } from '../../requestidlecallback';

let realIntlTelInput;
let loadCalled = false;
async function intlTelInput(a, b = undefined) {
    if (!loadCalled) {
        // Only load if the page gets interaction
        await new Promise((resolve) => {
            window.addEventListener('scroll', resolve, { once: true, passive: true });
            document.addEventListener('click', resolve, { once: true, passive: true });
            document.addEventListener('keydown', resolve, { once: true, passive: true });
        });
    }

    const intlTelInputLib = await loadLib();
    return intlTelInputLib(a, b);
}

async function loadLib() {
    if (realIntlTelInput != null) return realIntlTelInput;

    if (!loadCalled) {
        import('./intl-tel-input-flags');
        loadCalled = true;
    }

    const lib = await import('intl-tel-input');
    realIntlTelInput = lib.default;

    requestIdleCallback(() => {
        if (window.intlTelInputGlobals.startedLoadingUtilsScript) return;
        window.intlTelInputGlobals.startedLoadingUtilsScript = true;

        import('intl-tel-input/build/js/utils');
    });
    
    return realIntlTelInput;
}

export default intlTelInput;

// import '../../jquery';
import '../vendor/bootstrap';
import '../vendor/font-awesome';

import './common.purged.css';
import './style-res.purged.css';
window.capitalize = (str, lower = false) =>
    (lower ? str.toLowerCase() : str).replace(/(?:^|\s|["'([{])+\S/g, (match) =>
        match.toUpperCase()
    );

if (window.hydrateJSON == null) {
    window.hydrateJSON = {};
}
var nextLocation = null;

function setupSlick() {
    //SPACE PAGE MEETING ROOMS SLIDER
    $('.space-meeting-rooms-outer').slick({
        dots: false,
        infinite: true,
        draggable: true,
        swipeToSlide: true,
        slidesToShow: 2,
        slidesToScroll: 1,
        responsive: [
            {
                breakpoint: 991,
                settings: {
                    slidesToShow: 2,
                },
            },
            {
                breakpoint: 767,
                settings: {
                    slidesToShow: 2,
                },
            },
            {
                breakpoint: 439,
                settings: {
                    slidesToShow: 1,
                },
            },
        ],
    });

    //NETWORK PAGE POPULAR LOCATIONS SLIDER
    $('.network-popular-spaces-slider').slick({
        dots: false,
        infinite: true,
        draggable: true,
        swipeToSlide: true,
        slidesToShow: 3,
        slidesToScroll: 1,
        responsive: [
            {
                breakpoint: 991,
                settings: {
                    slidesToShow: 3,
                },
            },
            {
                breakpoint: 767,
                settings: {
                    slidesToShow: 2,
                },
            },
            {
                breakpoint: 439,
                settings: {
                    slidesToShow: 1,
                },
            },
        ],
    });

    //HOME PAGE NEWEST FLEXIBLE OFFICE SPACES SLIDER
    $('.home-newest-flexible-office-slider').slick({
        dots: false,
        infinite: true,
        draggable: true,
        swipeToSlide: true,
        slidesToShow: 3,
        slidesToScroll: 1,
        responsive: [
            {
                breakpoint: 991,
                settings: {
                    slidesToShow: 3,
                },
            },
            {
                breakpoint: 767,
                settings: {
                    slidesToShow: 2,
                },
            },
            {
                breakpoint: 575,
                settings: {
                    slidesToShow: 1,
                },
            },
        ],
    });
}

//MOBILE NAVBAR
$(function () {
    $('.navbar-toggle').on('click', function () {
        $('main').toggleClass('nav-open');
        $('html').toggleClass('overflow-hidden');
    });
});

//DATEPICKER
window.toDate = (selectedDate) => {
    var from = selectedDate.split('/');
    return new Date(from[2], from[0] - 1, from[1]);
};

requestAnimationFrame(() => {
    import('../vendor/jquery-ui-datepicker').then(() => {
        const dateText = $('#date_today').val();
        const todayDate = dateText ? $.datepicker.parseDate('mm/dd/yy', dateText) : new Date();
        $(".datepicker").each(function () {
            let $this = $(this);
            if(!$this.hasClass('hasDatepicker')) {
                $this.datepicker({
                    minDate: todayDate,
                });
            }
        });
    });
});

$('.space-banner-outer').on('click', function () {
    $('#viewphotos').trigger('click');
});

/*SPACE REVIEW SHOW MORE*/
$('.review-more-less,.review-less-more').on('click', function () {
    $('.space-review-more-info-outer').toggle();
    $('.review-more-less').toggle();
    $('.review-less-more').toggle();
});

/*SPACE PAGE LESS MORE TOGGLE*/
$('.space-see-more a').on('click', function () {
    $(this).toggleClass('bttn-open');
    $('.see-more-content').toggleClass('open');
});

/*PRESS PAGE MORE LESS*/
$('.press-news-more-click a').on('click', function () {
    $(this).toggleClass('bttn-open');
    $('.press-news-see-more-content').toggleClass('open');
});

$('.press-release-more-click a').on('click', function () {
    $(this).toggleClass('bttn-open');
    $('.press-release-see-more-content').toggleClass('open');
});

$(function () {
    setupSignupPopup();
    setupLoginForm();
    setupSignupForm();
    setupNewsletterSignupForm();

    function validateEmail(email) {
        let re = /\S+@\S+\.\S+/;
        return re.test(email);
    }

    function validateInputEmail(requiredField, parentContainerClass) {
        let emailInput = $(requiredField).val();
        let hasError = false;

        if ($(requiredField).closest(parentContainerClass).length > 0) {
            if (emailInput.length > 0 && !validateEmail(emailInput)) {
                hasError = true;
                $(requiredField).siblings('.validation-error').show();
                emailInput = '';
            } else {
                $(requiredField).siblings('.validation-error').hide();
            }
        } else {
            emailInput = '';
        }
        return [hasError, emailInput];
    }

    function setupSignupPopup() {
        const facebookURL =
            window.hydrateJSON.facebook_url || $('#facebook_url').val();

        let signupPopup = $('#signup-popup');

        if (signupPopup.length === 0) {
            return;
        }

        let facebook_url_signup = $(signupPopup)
            .find('a.facebook-button-popup')
            .get(0);
        $(facebook_url_signup).attr('href', facebookURL);

        let signupPopupForm = $('#signup-form-popup');

        if (signupPopupForm.length === 0) {
            return;
        }

        let facebook_url_signup_form = $(signupPopupForm)
            .find('a.facebook-button-popup')
            .get(0);
        $(facebook_url_signup_form).attr('href', facebookURL);
    }

    function setupLoginForm() {
        const facebookURL =
            window.hydrateJSON.facebook_url || $('#facebook_url').val();

        let loginFormPopup = $('#login-form-popup');
        if (loginFormPopup.length === 0) {
            return;
        }
        let loginFormPopupContainer = loginFormPopup.get(0);

        let form = $(loginFormPopupContainer).find('form')[0];

        $('.validation-error').hide();
        $('.modal').on('hidden.bs.modal', function () {
            $('.validation-error').hide();
        });

        $(loginFormPopupContainer)
            .find('a.login-popup-button')
            .get(0)
            .addEventListener('click', function () {
                submitLogin(form);
            });
        var facebook_url = $(loginFormPopupContainer)
            .find('a.facebook-button-popup')
            .get(0);
        $(facebook_url).attr('href', facebookURL);
    }

    function submitLogin(form) {
        const baseURL = window.hydrateJSON.baseURL || $('#base_url').val();
        $('.signup-lock').find('.validation-error').text('Email is required');
        let isValidLogin, params;
        [isValidLogin, params] = getValidatedLoginFormParams(form);

        if (isValidLogin) {
            grecaptcha.ready(function () {
                grecaptcha
                    .execute('6LcaVKAUAAAAAAfDTPgFv8tGuwrodh_Mv6_eJ0oT', {
                        action: 'validateNavLogin_a',
                    })
                    .then(function (captchaToken) {
                        params.captchaToken = captchaToken;
                        $.ajax({
                            url: baseURL + 'validate_navlogin',
                            type: 'POST',
                            dataType: 'json',
                            data: params,
                            success: function (response) {
                                if (response.msg == 'SCS') {
                                    if (nextLocation != null) {
                                        location = baseURL + nextLocation;
                                    } else {
                                        location.reload();
                                    }
                                } else {
                                    $(form)
                                        .find('.signup-lock')
                                        .find('.validation-error')
                                        .text(response.error);
                                    $(form)
                                        .find('.signup-lock')
                                        .find('.validation-error')
                                        .show();
                                }
                            },
                            error: function (msg) {},
                        });
                    });
            });
        }
    }

    function setupNewsletterSignupForm() {
        $('#newsletter_signup_button').on('click', function (e) {
            submitNewsletterForm();
        });
        function submitNewsletterForm() {
            const baseURL = window.hydrateJSON.baseURL || $('#base_url').val();

            let email = $('#newsletter_email');
            if (email.val().length == 0 || !validateEmail(email.val())) {
                $('#error_popop_message_container h2').html('');
                $('#error_popop_message_container p').html('Invalid email.');
                $('#error-popup').modal('show');
                return;
            } else {
                $(email).siblings('.validation-error').hide();
            }

            grecaptcha.ready(function () {
                grecaptcha
                    .execute('6LcaVKAUAAAAAAfDTPgFv8tGuwrodh_Mv6_eJ0oT', {
                        action: 'validateNewsletterSignup',
                    })
                    .then(function (captchaToken) {
                        let submitButton = $('#newsletter_signup_button');
                        submitButton.attr('disabled', true);
                        submitButton.attr(
                            'original-value',
                            submitButton.attr('value')
                        );
                        submitButton.attr('value', 'Processing...');
                        $.ajax({
                            url: baseURL + 'ajax/newsletter',
                            type: 'POST',
                            dataType: 'json',
                            data: {
                                email: email.val(),
                                captcha_token: captchaToken,
                            },
                            success: function (response) {
                                if (response.status == 'success') {
                                    email.val('');
                                    $(
                                        '#success_popop_message_container p'
                                    ).html(
                                        "You're now subscribed to our newsletter! We'll keep you posted with out latest updates."
                                    );
                                    $('#success-popup').modal('show');
                                    submitButton.attr(
                                        'value',
                                        submitButton.attr('original-value')
                                    );
                                    submitButton.attr('disabled', false);
                                } else {
                                    $('#error_popop_message_container h2').html(
                                        ''
                                    );
                                    $('#error_popop_message_container p').html(
                                        response.field_message
                                    );
                                    $('#error-popup').modal('show');
                                    submitButton.attr(
                                        'value',
                                        submitButton.attr('original-value')
                                    );
                                    submitButton.attr('disabled', false);
                                }
                            },
                            error: function (msg) {
                                $('#error-popup').modal('show');
                                submitButton.attr(
                                    'value',
                                    submitButton.attr('original-value')
                                );
                                submitButton.attr('disabled', false);
                            },
                        });
                    });
            });
        }
    }

    function getValidatedLoginFormParams(form) {
        let hasErrors = false;
        let params = {};

        $(form)
            .find('.signup-lock')
            .find('.validation-error')
            .text('Password is required');

        $(form)
            .find('input')
            .filter('[is_required]')
            .each(function (i, requiredField) {
                if ($.trim($(requiredField).val()) === '') {
                    $(requiredField).siblings('.validation-error').show();
                    hasErrors = true;
                } else {
                    if (
                        $(requiredField).closest('div.signup-user').length > 0
                    ) {
                        [hasErrors, params.semail] = validateInputEmail(
                            requiredField,
                            'div.signup-user'
                        );
                    } else {
                        params.spass = $(requiredField).val();
                        $(requiredField).siblings('.validation-error').hide();
                    }
                }
            });

        if (!hasErrors) {
            params.form_login = 1;
            params.msg_log = 0;
            return [true, params];
        } else {
            return [false, params];
        }
    }

    function setupSignupForm() {
        let signupFormPopup = $('#signup-form-popup');
        if (signupFormPopup.length === 0) return;
        let signupFormPopupContainer = signupFormPopup.get(0);

        let form = $(signupFormPopupContainer).find('form')[0];

        $('.validation-error').hide();
        $('.modal').on('hidden.bs.modal', function () {
            $('.validation-error').hide();
        });

        $(signupFormPopupContainer)
            .find('div.signup-now-button')
            .children()
            .get(0)
            .addEventListener('click', function () {
                submitSignup(form);
            });
    }

    function submitSignup(form) {
        let isValidLogin, params;
        [isValidLogin, params] = getValidatedSignupFormParams(form);

        if (isValidLogin) {
            grecaptcha.ready(function () {
                grecaptcha
                    .execute('6LcaVKAUAAAAAAfDTPgFv8tGuwrodh_Mv6_eJ0oT', {
                        action: 'validateNavSignup_a',
                    })
                    .then(function (captchaToken) {
                        params.captchaToken = captchaToken;
                        window.hydrateJSON = window.hydrateJSON || {};
                        const baseURL =
                            window.hydrateJSON.baseURL || $('#base_url').val();

                        $.ajax({
                            url: baseURL + '/validate_navsignup',
                            type: 'POST',
                            dataType: 'json',
                            data: params,
                            success: function (response) {
                                if (response.msg == 'SCS') {
                                    location.reload();
                                } else {
                                    $(form)
                                        .find('.signup-envelope')
                                        .find('.validation-error')
                                        .text(response.error);
                                    $(form)
                                        .find('.signup-envelope')
                                        .find('.validation-error')
                                        .show();
                                }
                            },
                            error: function (msg) {},
                        });
                    });
            });
        }
    }

    function getValidatedSignupFormParams(form) {
        let hasErrors = false;
        let params = {};

        $(form)
            .find('.signup-lock')
            .find('.validation-error')
            .text('Password is required');
        $(form)
            .find('.signup-envelope')
            .find('.validation-error')
            .text('Email is required');

        $(form)
            .find('input')
            .filter('[is_required]')
            .each(function (i, requiredField) {
                if ($.trim($(requiredField).val()) === '') {
                    $(requiredField).siblings('.validation-error').show();
                    hasErrors = true;
                } else {
                    let parentContainerClass = $(requiredField)
                        .parent()
                        .prop('className')
                        .replace('signup-input-outer ', '');
                    switch (parentContainerClass) {
                        case 'signup-firstname':
                            $(requiredField)
                                .siblings('.validation-error')
                                .hide();
                            params.fname = $.trim($(requiredField).val());
                            break;
                        case 'signup-lastname':
                            $(requiredField)
                                .siblings('.validation-error')
                                .hide();
                            params.lname = $.trim($(requiredField).val());
                            break;
                        case 'signup-company':
                            $(requiredField)
                                .siblings('.validation-error')
                                .hide();
                            params.cname = $.trim($(requiredField).val());
                            break;
                        case 'signup-envelope':
                            let isValidEmail;
                            const [isInvalidEmail, email] = validateInputEmail(
                                requiredField,
                                'div.signup-envelope'
                            );
                            hasErrors = isInvalidEmail;
                            if (isInvalidEmail) {
                                $(requiredField)
                                    .siblings('.validation-error')
                                    .show();
                            } else {
                                $(requiredField)
                                    .siblings('.validation-error')
                                    .hide();
                                params.semail = $.trim($(requiredField).val());
                            }
                            break;
                        case 'signup-lock':
                            $(requiredField)
                                .siblings('.validation-error')
                                .hide();
                            params.spass = $.trim($(requiredField).val());
                            break;
                        case 'signup-lock-confirm':
                            if ($('div.signup-lock-confirm input').val().trim() === $('div.signup-lock input').val().trim()) {
                                $(requiredField)
                                    .siblings('.validation-error')
                                    .hide();
                            } else {
                                hasErrors = true;
                                $(requiredField)
                                    .siblings('.validation-error')
                                    .show();
                            }
                            break;
                        default:
                    }
                }
            });
        if (!hasErrors) {
            params.form_signup = 1;
            params.msg_log = 1;
            return [true, params];
        } else {
            return [false, params];
        }
    }
});
//SELECT FIELD ON SEARCH PAGE VIEWFILTER MEMBERS NUMBER
/*$(function () {
    $('.makeMeList').each(function (index, element) {
        $(this).parent()
            .after()
            .append("<div class='scrollableList'><div class='selectedOption'></div><ul></ul></div>");

        $(element).each(function (idx, elm) {
            $('option', elm).each(function (id, el) {
                $('.scrollableList ul:last').append('<li>' + el.text + '</li>');
            });
            $('.scrollableList ul').hide();
            $('.makeMeUl').children('div.selectedOption').text("Select");
        });
        $('.scrollableList:last').children('div.selectedOption').text("Select");
    });

    $('.selectedOption').on('click', function () {
        $(this).next('ul').slideToggle(200);
        $('.selectedOption').not(this).next('ul').hide();
    });

    $('.scrollableList ul li').on('click', function () {
        var selectedLI = $(this).text();
        $(this).parent().prev('.selectedOption').text(selectedLI);
        $(this).parent('ul').hide();
    });

    $('.scrollableList').show();
    $('.makeMeList').hide();
}); */

//DURATION ACTIVE
$(function () {
    $('.search-left-duration-con .looking-for-inner .looking-radio-con').on(
        'click',
        function () {
            var current_div = $(this);
            if (current_div.children('.home-input-radio').is(':checked')) {
                //alert('checked');
                current_div.addClass('active');
            } else {
                //alert('unchecked');
                current_div.removeClass('active');
            }
        }
    );

    $('.search-left-duration-con .looking-for-inner .looking-radio-con').each(
        function () {
            var current_div = $(this);
            if (current_div.children('.home-input-radio').is(':checked')) {
                //alert('checked');
                current_div.addClass('active');
            } else {
                //alert('unchecked');
                current_div.removeClass('active');
            }
        }
    );
});

$('.search-globalpass-cross').on('click', function () {
    $('.search-map-global-pass-outer').toggleClass('hide');
});

function selectProp() {
    //SELECT BOX
    $('select').each(function () {
        var $this = $(this),
            numberOfOptions = $(this).children('option').length;

        $this.addClass('select-hidden');
        $this.wrap('<div class="select"></div>');
        $this.after('<div class="select-styled unselect-text"></div>');

        var $styledSelect = $this.next('div.select-styled');

        //$styledSelect.text($this.children('option:selected').text());
        $styledSelect.text($this.children('option').eq(0).text());
        var $list = $('<ul />', {
            class: 'select-options',
        }).insertAfter($styledSelect);
      
        const startFrom =
          $this.attr('name')?.includes('search_form_capacity') ||
            $this.attr('name')?.includes('search_form_duration_metrics') ||
              $this.attr('name')?.includes('search_form_duration') ? 0 : 1;
      
        if ($this.attr('name')?.includes('search_form_duration_metrics')) {
          $styledSelect.text($this.children('option:selected').text());
        }

        for (var i = startFrom; i < numberOfOptions; i++) {
            $('<li />', {
                text: $this.children('option').eq(i).text(),
                rel: $this.children('option').eq(i).val(),
            }).appendTo($list);
        }

        var $listItems = $list.children('li');

        $styledSelect.on('click', function (e) {
            e.stopPropagation();
            $('div.select-styled.active')
                .not(this)
                .each(function () {
                    $(this)
                        .removeClass('active')
                        .next('ul.select-options')
                        .hide();
                });
            $(this).toggleClass('active').next('ul.select-options').toggle();
        });

        $listItems.on('click', function (e) {
            e.stopPropagation();
            $styledSelect.text($(this).text()).removeClass('active');
            $this.val($(this).attr('rel'));
            $this.trigger('change');
            $list.hide();
            if ($this.val() == '') {
                $listItems
                    .parent()
                    .siblings('.select-styled')
                    .addClass('unselect-text');
            } else {
                $listItems
                    .parent()
                    .siblings('.select-styled')
                    .removeClass('unselect-text');
            }
        });

        $(document).on('click', function () {
            $styledSelect.removeClass('active');
            $list.hide();
        });
    });
}

export function selectRebuildOptions(selectElement, selectedFixOnly) {
    let jQueryElementList = [];
    if (typeof selectElement === 'string') {
        jQueryElementList = $('#' + selectElement);
    } else if (selectElement instanceof jQuery) {
        jQueryElementList = selectElement;
    } else {
        return;
    }
    let selectElementList = jQueryElementList.filter('select');
    //SELECT BOX
    selectElementList.each(function () {
        var $this = $(this);
        var $options = $(this).children('option');
        var numberOfOptions = $options.length;

        var $styledSelect = $this.next('div.select-styled');
        // We really need to just use HTML select, this is unnecessary complexity
        var $selectedOption = $options
            .filter(function () {
                return this.hasAttribute('selected');
            })
            .eq(0);
        var text = $options.eq(0).text();
        if ($selectedOption.length > 0) {
            text = $selectedOption.text();
            $this.val($selectedOption.val());
        }

        $styledSelect.text(text);
        if (selectedFixOnly) return;

        var $list = $this.parent().find('ul.select-options');
        $list.empty();

        for (var i = 0; i < numberOfOptions; i++) {
            $('<li />', {
                text: $options.eq(i).text(),
                rel: $options.eq(i).val(),
            }).appendTo($list);
        }

        var $listItems = $list.children('li');

        $listItems.on('click', function (e) {
            e.stopPropagation();
            $styledSelect.text($(this).text()).removeClass('active');
            $this.val($(this).attr('rel'));
            $list.hide();
            $this.trigger('change');
            if ($this.val() == '') {
                $listItems
                    .parent()
                    .siblings('.select-styled')
                    .addClass('unselect-text');
            } else {
                $listItems
                    .parent()
                    .siblings('.select-styled')
                    .removeClass('unselect-text');
            }
        });

        $(document).on('click', function () {
            $styledSelect.removeClass('active');
            $list.hide();
        });
    });
}

selectProp();

let resetSubmitting = false;
function resetPassword(evt) {
    evt.preventDefault();
    resetSubmitting = true;
    const baseURL = hydrateJSON.baseURL || $('#base_url').val();
    $('#msg-reset-password-none').hide()
    $('#msg-reset-password-unregistered').hide();
    $('#msg-reset-password-invalid').hide();
    grecaptcha.ready(function () {
        grecaptcha.execute(
            '6LcaVKAUAAAAAAfDTPgFv8tGuwrodh_Mv6_eJ0oT',
            { action: 'forgot_password_a' }
        ).then(function (captchaToken) {
            var email = $("#email-reset").val();
            var captchaToken = captchaToken;
            $.post(baseURL + "api/v2/i/request-reset-password",
                {
                    email: email,
                    captchaToken: captchaToken
                },
              function (data) {
                    if (!data) {
                      // nothing printed in email field
                      $('#msg-reset-password-none').show();
                    } else if (data.msg === 'fail') {
                        // any fail reason
                        $('#msg-reset-password-unregistered').show();
                    } else if (data.msg === 'scs') {
                        // success
                        $('#email-reset-address').text(email);
                        $('#email-reset-address').attr('href', 'mailto:' + email);
                        $('#reset-password-form-popup').modal('hide');
                        $('#email-reset-passowrd-popup').modal('show');
                        $('#email-reset').val('');
                    }
                }
            );
        });
    });
}

$(function () {
    $('#email-reset-address').on('click', function (e) { e.preventDefault(); });

    $('#error-popup-close-button').on('click', function () {
        $('#error-popup').modal('hide');
    });

    $('#success-popup-close-button').on('click', function () {
        $('#success-popup').modal('hide');
    });

    $('#form-reset-password').on('submit', resetPassword);

    $('#rest-password-button').on('click', function () {
        $("#login-form-popup").modal("hide");
    });

    $("#submit-reset-password").on('click', resetPassword);

    $('#popup-signup-button02').on('click', function () {
        $('#signup-popup').modal('hide');
    });

    $('#popup-signup-button').on('click', function () {
        $('#login-form-popup').modal('hide');
    });

    $('#already-login-popup02').on('click', function () {
        $('#signup-form-popup').modal('hide');
    });

    $('#already-login-popup').on('click', function () {
        $('#signup-popup').modal('hide');
    });

    $('#rest-password-button').on('click', function () {
        $('#login-form-popup').modal('hide');
    });

    $('#email-reset-password').on('click', function () {
        $('#reset-password-invalid-requests').modal('hide');
    });

    $('.search-globalpass-cross').on('click', function () {
        $('.search-map-global-pass-outer').animate({ height: 0 }, 1000);
    });

    $('.admin-portal-login').on('click', function () {
        $('.adminportal-profile-hover').slideToggle();
    });

    $('#signupme').on('click', function () {
        $('.footer-error-success').show();
    });

    $('.space-language0-tab').on('click', function () {
        $('.space-language0-description').show();
        $('.space-language1-description').hide();
        $('.space-language0-tab').addClass('space-language-active');
        $('.space-language1-tab').removeClass('space-language-active');
    });

    $('.space-language1-tab').on('click', function () {
        $('.space-language0-description').hide();
        $('.space-language1-description').show();
        $('.space-language0-tab').removeClass('space-language-active');
        $('.space-language1-tab').addClass('space-language-active');
    });
 $('.press-news-tab').on('click', function () {
        $('#press-news-content').show();
        $('#press-releases-content').hide();
        $('.press-news-tab').addClass('press-tab-active');
        $('.press-releases-tab').removeClass('press-tab-active');
    });

    $('.press-releases-tab').on('click', function () {
        $('#press-news-content').hide();
        $('#press-releases-content').show();
        $('.press-news-tab').removeClass('press-tab-active');
        $('.press-releases-tab').addClass('press-tab-active');
    });

    $('.review-click-con').on('click', function () {
        $('.space-green-heart').hide();
        $('.review-click-con span').hide();
        $('.space-red-heart').show();
        $('.review-votes-con').show();
        $('.reviews-thanks-con').addClass('reviews-red-color');
    });

    $('.review-click-con02').on('click', function () {
        $('.space-green-heart').hide();
        $('.review-click-con02 span').hide();
        $('.space-red-heart').show();
        $('.review-votes-con').show();
        $('.reviews-thanks-con').addClass('reviews-red-color');
    });

    //PRICING PAGE ACCORDION
    function toggleIcon(e) {
        $(e.target)
            .prev('.panel-heading')
            .find('.more-less')
            .toggleClass('fa-minus fa-plus');
    }

    $('.panel-group').on('hidden.bs.collapse', toggleIcon);
    $('.panel-group').on('shown.bs.collapse', toggleIcon);

    $(function () {
        $('.pricing-faq-main-outer .panel.panel-default').on(
            'click',
            function () {
                // remove the class from the currently selected
                $('.pricing-faq-main-outer .panel.panel-default').removeClass(
                    'pricing-active'
                );
                // add the class to the newly clicked link
                $(this).addClass('pricing-active');
                if (!$(this).addClass('pricing-active')) {
                } else {
                    $(this).addClass('pricing-active');
                    $(this)
                        .next()
                        .stop(true, true)
                        .removeClass('pricing-active');
                }
            }
        );

        $('.review-goback-con a').on('click', function () {
            // remove the class from the currently selected
            $('.review-goback-con a').removeClass('review-goback-button');
            // add the class to the newly clicked link
            $(this).addClass('review-goback-button');
            if (!$(this).addClass('review-goback-button')) {
            } else {
                $(this).addClass('review-goback-button');
                $(this)
                    .next()
                    .stop(true, true)
                    .removeClass('review-goback-button');
            }
        });
    });

    $('.review-grey-star')
        .on('hover', function () {
            var current_div = this;
            var value = $(this).attr('data-value');

            $(this)
                .parent()
                .children('.review-grey-star')
                .children('i')
                .removeClass('rating-focus');
            $(this)
                .parent()
                .children('.review-grey-star')
                .children('i')
                .addClass('rating-unfocus');

            for (var i = 1; i <= value; i++) {
                $(this)
                    .parent()
                    .children('[data-value="' + i + '"]')
                    .children('i')
                    .addClass('rating-focus');

                $(this)
                    .parent()
                    .children('[data-value="' + i + '"]')
                    .children('i')
                    .removeClass('rating-unfocus');
            }

            $(current_div)
                .parent()
                .children('.review-grey-star')
                .addClass('review-status-show-focus-out');

            $(current_div).addClass('review-status-show-focus');
            $(current_div).removeClass('review-status-show-focus-out');
        })
        .on('mouseleave', function () {
            var current_div = this;

            $(this)
                .parent()
                .children('.review-grey-star')
                .children('i')
                .removeClass('rating-focus');

            $(this)
                .parent()
                .children('.review-grey-star')
                .children('i')
                .removeClass('rating-unfocus');

            $(current_div)
                .parent()
                .children('.review-grey-star')
                .removeClass('review-status-show-focus');

            $(current_div)
                .parent()
                .children('.review-grey-star')
                .removeClass('review-status-show-focus-out');
        })
        .on('click', function () {
            var current_div = this;
            var value = $(this).attr('data-value');

            $(this)
                .parent()
                .children('.review-grey-star')
                .children('i')
                .removeClass('rating-active');

            for (var i = 1; i <= value; i++) {
                $(this)
                    .parent()
                    .children('[data-value="' + i + '"]')
                    .children('i')
                    .addClass('rating-active');
            }

            $(current_div)
                .parent()
                .children('.review-grey-star')
                .removeClass('review-staus-show');

            $(current_div).addClass('review-staus-show');
        });

    /*$('.review-grey-star i').on('click', function(){
            $('.review-grey-star').removeClass('review-staus-show');
            $(this).parent('.review-grey-star').addClass('review-staus-show');
        });*/
});

let flagLoaded = false;
function loadFlag(){
    let options = {
        threshold: 0.25,
    };
    if (flagLoaded) return;

    const observer = new IntersectionObserver((entries) => {
        for (let entry of entries) {
            if (!entry.isIntersecting) continue;
            flagLoaded = true;
            import('./flag');
            observer.disconnect();
            break;
        }
    }, options);

    observer.observe(document.querySelector('.flag'));
}
loadFlag();
requestAnimationFrame(() => {
    import('./search');
});
requestAnimationFrame(() => {
    import('../vendor/slick').then(() => {
        window.dispatchEvent(new Event('slick-ready'));
        setupSlick();
    });
});
window.addEventListener('scroll', () => {
    $('.never-miss-updates-outer-panel').show();
}, {once: true, passive: true});

let recaptchaLoaded = false;
// Only want to load ReCaptcha when a user actually interacts, it's over 250KB compressed
function loadRecaptcha() {
    if (recaptchaLoaded) return;
    recaptchaLoaded = true;

    const script = document.createElement("script");
    script.src = 'https://www.google.com/recaptcha/api.js?render=6LcaVKAUAAAAAAfDTPgFv8tGuwrodh_Mv6_eJ0oT';
    script.async = true;
    document.head.appendChild(script);
}

window.addEventListener('scroll', loadRecaptcha, {once: true, passive: true});
document.addEventListener('click', loadRecaptcha, {once: true, passive: true});
document.addEventListener('keydown', loadRecaptcha, {once: true, passive: true});
