# Watermark-FPDF
```php
    composer require kristianlentino/watermark-fpdf
```
Permette di creare facilmente un watermark in un file PDF.
Esempio:

 ```php
        use Kristianlentino\WatermarkFpdf\WatermarkFpdi;
        $fpdi = new WatermarkFpdi();
		$pdfPath = __DIR__. DIRECTORY_SEPARATOR.'..'.DIRECTORY_SEPARATOR.'../media/lf_ebooks/1634655065/file.pdf';
		$pdfPathSave = __DIR__. DIRECTORY_SEPARATOR.'..'.DIRECTORY_SEPARATOR.'../media/lf_ebooks/1634655065/file_prova.pdf';
		$pageCount = $fpdi->setSourceFile($pdfPath);
		for ($pageNo = 1; $pageNo <= $pageCount; $pageNo++) {

			// import a page
			$templateId = $fpdi->importPage($pageNo);
			$size = $fpdi->getTemplateSize($templateId);
			//set the new page to the size of the template
			$fpdi->AddPage('',[$size['width'],$size['height']]);

			//the last parameter will adjust the size of the page
			$fpdi->useTemplate($templateId, 0, 0, null, null, true);

			// set alpha to semi-transparency
			$fpdi->SetAlpha(0.5);
			$fpdi->SetFont('Arial','B',80);
			$fpdi->SetTextColor(188,190,190);
			$fpdi->RotatedText(50,180,'Lavorofacile',45);
			// set alpha to semi-transparency
			$fpdi->SetAlpha(1);
		}

        /* 
            I --> mostra il file nel browser,
            D --> Download file 
            F --> Salva il file in locale 
            S --> Ritorna il file come stringa 
        */
		return $fpdi->Output($pdfPathSave,'I');
```

Queste funzioni sono state prese dai seguenti link:
 - http://www.fpdf.org/en/script/script9.php
 - http://www.fpdf.org/en/script/script2.php
 - http://www.fpdf.org/en/script/script74.php