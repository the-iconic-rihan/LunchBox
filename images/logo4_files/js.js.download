$(function () {
    $(".logo-image").error(function () {
        $(this).attr('src', '/img/image-not-found.png');
    });
    $('#searchBarInput').keypress(function (event) {
        if (event.keyCode == 13) {
            $('#searchBarButton').click();
            return false;
        }
    });
    $('#checkBoxRegisterShowPassword').change(function () {
        if ($('#checkBoxRegisterShowPassword').prop('checked')) $('#textBoxRegisterPassword').attr('type', 'text');
        else $('#textBoxRegisterPassword').attr('type', 'password');
    });
    $('#buttonRegister').click(function () {
        if ($('#formRegister').valid()) {
            $('#checkBoxRegisterShowPassword').prop('checked', false);
            $('#textBoxRegisterPassword').attr('type', 'password');
            $('#buttonRegister').css('background-color', '#A2C5D6');
            $('#buttonRegister').css('cursor', 'default');
            $('#buttonRegister').attr('disabled', true);
            $('#buttonRegister').html('<i class="fa fa-spinner fa-lg fa-pulse form-button-icon"></i>');

            __doPostBack('M$C$buttonRegister', 'Click');
        }
    });
    $('#buttonLogin').click(function () {
        if ($('#formRegister').valid()) {
            $('#buttonLogin').css('background-color', '#A2C5D6');
            $('#buttonLogin').css('cursor', 'default');
            $('#buttonLogin').attr('disabled', true);
            $('#buttonLogin').html('<i class="fa fa-spinner fa-lg fa-pulse form-button-icon"></i>');

            __doPostBack('M$C$buttonLogin', 'Click');
        }
    });
    $('#buttonRecoverPassword').click(function () {
        if ($('#formRegister').valid()) {
            $('#buttonRecoverPassword').css('background-color', '#A2C5D6');
            $('#buttonRecoverPassword').css('cursor', 'default');
            $('#buttonRecoverPassword').attr('disabled', true);
            $('#buttonRecoverPassword').html('<i class="fa fa-spinner fa-lg fa-pulse form-button-icon"></i>');

            __doPostBack('M$C$buttonRecoverPassword', 'Click');
        }
    });
    $('.loginFormLink').click(function () {
        $('#registerForm').hide();
        $('#forgotPasswordForm').hide();
        $('#loginForm').fadeIn(500);
    });
    $('.registerFormLink').click(function () {
        $('#loginForm').hide();
        $('#forgotPasswordForm').hide();
        $('#registerForm').fadeIn(500);
    });
    $('.forgotPasswordFormLink').click(function () {
        $('#registerForm').hide();
        $('#loginForm').hide();
        $('#forgotPasswordForm').fadeIn(500);
    });
    $('#textBoxLoginUserName, #textBoxLoginPassword').keypress(function (event) {
        if (event.keyCode == 13) {
            $('#buttonLogin').click();
            return false;
        }
    });
    $('#buttonUpload').click(function () {
        if ($('#formUpload').valid()) {
            $('#buttonUpload').css('background-color', '#A2C5D6');
            $('#buttonUpload').css('cursor', 'default');
            $('#buttonUpload').attr('disabled', true);
            $('#buttonUpload').html('<i class="fa fa-spinner fa-lg fa-pulse form-button-icon"></i> Uploading...');

            __doPostBack('M$C$buttonUpload', 'Click');
        }
    });
    function logoRateBind(rate) {
        if ($('#hiddenFieldRated').val().split('|')[0] == "0") {
            for (var i = 1; i <= 5; i++) {
                if (i <= rate) $('.logo-rate-' + i.toString()).attr("src", "/img/icon-rate-star-2.png");
                else $('.logo-rate-' + i.toString()).attr("src", "/img/icon-rate-star.png");
            }
        }
    }
    $('*[class^="logo-rate-"]').hover(function () {
            var rate = $(this).attr("class").replace("logo-rate-", "");
            logoRateBind(rate)
        }, function () {
            var rate = $('#hiddenFieldRated').val().split('|')[1];
            logoRateBind(rate);
        }
    );
    $('*[class^="logo-rate-"]').click(function () {
        if ($('#hiddenFieldRated').val().split('|')[0] == "0") {
            var rate = $(this).attr("class").replace("logo-rate-", "");
            $('#hiddenFieldRated').val('1|' + rate);
            $('.detail-rate-message').html("Thanks for voting!");

            $.post("/api.aspx", {
                page: 'rateLogo', rate: rate, logo: $('#hiddenFieldId').val()
            });
        }
    });
    $('#feedbackMessage').limiter(300, "");
    $('.feedback-header').click(function () {
        $('#feedbackSent').html("");
        if ($('.feedback-header').hasClass('open-fb')) {
            $('.feedback-wrapper').stop().animate({ marginBottom: 0 });
        }
        else {
            $('.feedback-wrapper').stop().animate({ marginBottom: -220 });
        }
        $('.feedback-header').toggleClass('open-fb close-fb');
    });
    function feedbackRateBind(rate) {
        for (var i = 1; i <= 5; i++) {
            if (i <= rate) $('.feedback-rate-' + i.toString()).attr("src", "/img/icon-feedback-rate.png");
            else $('.feedback-rate-' + i.toString()).attr("src", "/img/icon-feedback-rate-2.png");
        }
        if (rate != 0) $('#feedbackRateText').text(rate.replace("1", "Poor").replace("2", "Fair").replace("3", "Good").replace("4", "Very Good").replace("5", "Excellent"));
        else $("#feedbackRateText").text("");
    }
    $('*[class^="feedback-rate-"]').hover(
        function () {
            if ($(this).attr("disabled") != true) {
                var rate = $(this).attr("class").replace("feedback-rate-", "");
                feedbackRateBind(rate);
            }
        }, function () {
            if ($(this).attr("disabled") != true) {
                var rate = $('#feedbackRate').val();
                feedbackRateBind(rate);
            }
        }
    );
    $('*[class^="feedback-rate-"]').click(function () {
        var rate = $(this).attr("class").replace("feedback-rate-", "");
        $('#feedbackRate').val(rate);
    });
    $('#feedbackButton').click(function () {
        if ($('#feedbackRate').val() != "0") {
            $("#feedbackSent").html("Thank you for feedback!");
            $(this).attr("disabled", true);
            $.post("/api.aspx", {
                page: 'feedback', rate: $('#feedbackRate').val(), message: $('#feedbackMessage').val(), referer: $('#feedbackReferer').val()
            }).always(function () {
                setTimeout(function () {
                    $('.feedback-wrapper').stop().animate({ marginBottom: -220 });
                    $('.feedback-header').toggleClass('open-fb close-fb');
                }, 2000);
                setTimeout(function () {
                    $('#feedbackMessage').val("");
                    $('#feedbackButton').removeAttr('disabled');
                    $('#feedbackRate').val(0);
                    feedbackRateBind(0);
                }, 3000);
            });
        }
        else {
            $('.rate-icon-group').highlight();
            $("#feedbackRateText").text("Please rate");
        }
    });
    $('.feedback-close').click(function () {
        $('.feedback-wrapper').hide();
        document.cookie = "feedbackHide=1";
    });
    $('.track-shutterstock').on('click', function () {
        ga('send', 'event', 'Ad', 'click', 'ShutterStock', { 'transport': 'beacon' });
    });
    $('.track-shutterstock-coupon').on('click', function () {
        ga('send', 'event', 'Ad', 'click', 'ShutterStock-Coupon', { 'transport': 'beacon' });
    });
});
function searchFilter() {
    var url = baseUrl;
    if (url.indexOf('?') > -1) url += "&";
    else url += "?";
    var events = [];
    var queryArray = ["sort,filterSortGroup", "filter,filterTypeGroup", "format,filterFormatGroup", "color,filterColorGroup"];
    for (var i = 0; i < queryArray.length; ++i) {
        var queryName = queryArray[i].split(',')[0];
        var inputName = queryArray[i].split(',')[1];
        var queryValues = $.map($('input[name="' + inputName + '"]:checked'), function (c) { return c.value; }).join(",");
        if (queryValues) {
            url += queryName + "=" + queryValues + "&";
            if (queryName != "sort") events.push(queryName);
        }
    }

    ga('send', { hitType: 'event', eventCategory: 'FilterForm', eventAction: events.join(",").replace("filter", "type"), eventLabel: 'Filter' });
    if (url.trim().substr(url.trim().length - 1) == "&") url = url.trim().slice(0, -1);
    window.location = url;
}
function searchFilterRemoveValue(removeName, removeValue) {
    var url = baseUrl;
    if (url.indexOf('?') > -1) url += "&";
    else url += "?";
    var queryArray = ["sort", "filter", "format", "color"];
    for (var i = 0; i < queryArray.length; ++i) {
        var queryValues = $.QueryString[queryArray[i]];
        if (removeName == queryArray[i]) {
            var valueArray = queryValues.split(",");
            if (valueArray.indexOf(removeValue) !== (-1)) valueArray.splice(valueArray.indexOf(removeValue), 1);
            if (valueArray.join(",")) url += removeName + "=" + valueArray.join(",") + "&";
        }
        else if (queryValues) url += queryArray[i] + "=" + queryValues + "&";
    }

    if (url.trim().substr(url.trim().length - 1) == "&") url = url.trim().slice(0, -1);
    window.location = url;
}
function searchFilterClear() {
    window.location = baseUrl;
}
function searchPopup(keyword) {
    if (isCookieEnabled()) {
        if (document.cookie.indexOf("ad_popup=1") < 0) {
            document.cookie = "ad_popup=1";
            var keywordSlug = keyword;
            if (typeof getSlug === "function") {
                keywordSlug = getSlug(keyword, { separator: ' ' })
            }
            window.open('https://shutterstock.7eer.net/Az2K?sharedid=pop-up&subId1=popup&subId2=' + keywordSlug + '&subId3=popup&u=https%3A%2F%2Fwww.shutterstock.com%2Fsearch%2F' + keywordSlug, 'ShutterStock', 'width=' + $(window).width() * 0.5 + ',height=' + $(window).height() * 0.5 + ',toolbar=0,menubar=0,location=0,status=1,scrollbars=1,resizable=1,left=300,top=250');
            ga('send', 'event', 'Ad', 'open', 'ShutterStock-Popup', { 'transport': 'beacon' });
        }
    }
}
function shareTwitter(page) { window.open(page, "shareTwitter", "height=400,width=550,resizable=1,toolbar=0,menubar=0,status=0,location=0"); }
function shareFacebook(page) { window.open(page, "shareFacebook", "height=380,width=660,resizable=0,toolbar=0,menubar=0,status=0,location=0,scrollbars=0"); }
function sharePinterest(page) { window.open(page, "sharePinterest", "height=270,width=630,resizable=0,toolbar=0,menubar=0,status=0,location=0,scrollbars=0"); }
function isCookieEnabled() {
    try {
        // Create cookie
        document.cookie = 'cookietest=1';
        var ret = document.cookie.indexOf('cookietest=') !== -1;
        // Delete cookie
        document.cookie = 'cookietest=1; expires=Thu, 01-Jan-1970 00:00:01 GMT';
        return ret;
    }
    catch (e) {
        return false;
    }
}
function isNumeric(n) {
    return !isNaN(parseFloat(n));
}
function increaseIntCookie(cookieName, num) {
    if (isCookieEnabled()) {
        if (isNumeric(Cookies.get(cookieName))) {
            Cookies.set(cookieName, parseFloat(Cookies.get(cookieName)) + num);
        }
        else Cookies.set(cookieName, num);
    }
}
(function ($) {
    $.fn.extend({
        limiter: function (limit, elem) {
            $(this).on("keyup focus", function () {
                setCount(this, elem);
            });
            function setCount(src, elem) {
                var chars = src.value.length;
                if (chars > limit) {
                    src.value = src.value.substr(0, limit);
                    chars = limit;
                }
                if (elem != "") elem.html(chars + ' / ' + limit);
            }
            setCount($(this)[0], elem);
        }
    });

    $.QueryString = (function (a) {
        if (a == "") return {};
        var b = {};
        for (var i = 0; i < a.length; ++i) {
            var p = a[i].split('=', 2);
            if (p.length != 2) continue;
            b[p[0]] = decodeURIComponent(p[1].replace(/\+/g, " "));
        }
        return b;
    })(window.location.search.substr(1).split('&'))
})(jQuery);
jQuery.fn.highlight = function () {
    $(this).each(function () {
        var el = $(this);
        $("<div/>")
        .width(el.outerWidth())
        .height(el.outerHeight())
        .css({
            "position": "absolute",
            "left": el.offset().left,
            "top": el.offset().top,
            "background-color": "#F05F5C",
            "opacity": ".8",
            "z-index": "9999999"
        }).appendTo('body').fadeOut(500).queue(function () { $(this).remove(); });
    });
}