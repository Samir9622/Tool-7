<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Compression Tool | Reduce Image Size</title>
    <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6.4.0/css/all.min.css">
    <style>
        .drop-area {
            border: 2px dashed #3b82f6;
            transition: all 0.3s ease;
        }
        .drop-area.highlight {
            border-color: #10b981;
            background-color: rgba(16, 185, 129, 0.1);
        }
        .preview-img {
            max-height: 200px;
            object-fit: contain;
        }
        .slider {
            -webkit-appearance: none;
            height: 5px;
            border-radius: 5px;
            background: #d3d3d3;
            outline: none;
        }
        .slider::-webkit-slider-thumb {
            -webkit-appearance: none;
            appearance: none;
            width: 18px;
            height: 18px;
            border-radius: 50%;
            background: #3b82f6;
            cursor: pointer;
        }
        .slider::-moz-range-thumb {
            width: 18px;
            height: 18px;
            border-radius: 50%;
            background: #3b82f6;
            cursor: pointer;
        }
        .hidden {
            display: none;
        }
    </style>
</head>
<body class="bg-gray-50 text-gray-800 font-sans">
    <header class="bg-white shadow-md sticky top-0 z-10">
        <div class="container mx-auto px-4 py-4">
            <nav class="flex justify-between items-center">
                <a href="#" class="text-xl font-bold text-blue-600">Image Compression Tool</a>
                <ul class="flex space-x-4">
                    <li><a href="#" class="px-3 py-2 rounded hover:bg-blue-50 hover:text-blue-600">Home</a></li>
                    <li><a href="#" class="px-3 py-2 rounded hover:bg-blue-50 hover:text-blue-600">About</a></li>
                </ul>
            </nav>
        </div>
    </header>

    <main class="container mx-auto px-4 py-8">
        <section class="text-center mb-10">
            <h1 class="text-3xl font-bold text-blue-600 mb-3">Image Compression Tool</h1>
            <p class="text-lg text-gray-600">Reduce image size without losing quality</p>
        </section>

        <section class="bg-white rounded-lg shadow-md p-6 mb-10">
            <h2 class="text-2xl font-bold text-blue-600 text-center mb-6">Compress Your Images</h2>
            
            <div id="drop-area" class="drop-area rounded-lg p-10 text-center cursor-pointer mb-6">
                <i class="fas fa-cloud-upload-alt text-blue-500 text-4xl mb-4"></i>
                <p class="mb-2">Drag & Drop Your Images Here</p>
                <p class="text-gray-500 mb-4">Or</p>
                <button id="browse-button" class="bg-blue-600 text-white px-6 py-2 rounded-md hover:bg-blue-700 transition">Browse Files</button>
                <input type="file" id="file-input" accept="image/*" class="hidden" multiple>
            </div>

            <div class="mb-8 bg-gray-50 rounded-lg p-6">
                <h3 class="text-xl font-semibold text-blue-600 mb-4">Compression Settings</h3>
                
                <div class="mb-4">
                    <label for="quality" class="block mb-2 font-medium">Compression Level: <span id="quality-value">80</span>%</label>
                    <div class="flex items-center">
                        <span class="text-sm text-gray-500 mr-2">Higher Quality</span>
                        <input type="range" id="quality" class="slider flex-grow" min="0" max="100" value="80">
                        <span class="text-sm text-gray-500 ml-2">Smaller Size</span>
                    </div>
                </div>
                
                <div class="mb-4">
                    <label class="block mb-2 font-medium">Output Format</label>
                    <select id="format" class="w-full border border-gray-300 rounded px-3 py-2">
                        <option value="auto">Original Format</option>
                        <option value="jpeg">JPEG</option>
                        <option value="png">PNG</option>
                        <option value="webp">WebP</option>
                    </select>
                </div>
                
                <div class="flex items-center">
                    <input type="checkbox" id="maintain-dimensions" class="mr-2" checked>
                    <label for="maintain-dimensions">Maintain original dimensions</label>
                </div>
            </div>

            <!-- Preview Section -->
            <div id="preview-container" class="hidden mb-8">
                <h3 class="text-xl font-semibold text-blue-600 mb-4">Preview</h3>
                <div id="image-preview" class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <!-- Original and compressed images will be displayed here -->
                </div>
            </div>

            <!-- Results Section -->
            <div id="results-container" class="hidden mb-8">
                <h3 class="text-xl font-semibold text-blue-600 mb-4">Compression Results</h3>
                <div id="compression-results" class="space-y-4">
                    <!-- Compression results will be displayed here -->
                </div>
                <div class="mt-6 flex flex-wrap gap-3">
                    <button id="download-all" class="bg-blue-600 text-white px-4 py-2 rounded-md hover:bg-blue-700 transition">
                        <i class="fas fa-download mr-2"></i>Download All
                    </button>
                    <button id="download-zip" class="bg-green-600 text-white px-4 py-2 rounded-md hover:bg-green-700 transition">
                        <i class="fas fa-file-archive mr-2"></i>Download as ZIP
                    </button>
                </div>
            </div>
        </section>

        <section class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-10">
            <div class="bg-white rounded-lg shadow-md p-6 hover:shadow-lg transition">
                <h3 class="text-xl font-semibold text-blue-600 mb-3">Fast Processing</h3>
                <p>Our tool compresses your images in seconds using advanced algorithms to reduce file size without noticeable quality loss.</p>
            </div>
            <div class="bg-white rounded-lg shadow-md p-6 hover:shadow-lg transition">
                <h3 class="text-xl font-semibold text-blue-600 mb-3">Secure & Private</h3>
                <p>All image processing happens in your browser. Your files never leave your device, ensuring complete privacy.</p>
            </div>
            <div class="bg-white rounded-lg shadow-md p-6 hover:shadow-lg transition">
                <h3 class="text-xl font-semibold text-blue-600 mb-3">100% Free</h3>
                <p>No watermarks, no registration, no hidden fees. Compress as many images as you want, completely free.</p>
            </div>
        </section>
    </main>

    <footer class="bg-blue-600 text-white py-6">
        <div class="container mx-auto px-4 text-center">
            <p>© 2023 Image Compression Tool. All rights reserved.</p>
        </div>
    </footer>

    <!-- Loading Overlay -->
    <div id="loading-overlay" class="hidden fixed inset-0 bg-white bg-opacity-90 flex flex-col items-center justify-center z-50">
        <div class="w-12 h-12 border-4 border-blue-600 border-t-transparent rounded-full animate-spin mb-4"></div>
        <p id="loading-text">Processing images...</p>
    </div>

    <!-- Scripts -->
    <script src="https://cdn.jsdelivr.net/npm/compressorjs@1.1.1/dist/compressor.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/jszip@3.10.1/dist/jszip.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/file-saver@2.0.5/dist/FileSaver.min.js"></script>
    
    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const dropArea = document.getElementById('drop-area');
            const fileInput = document.getElementById('file-input');
            const browseButton = document.getElementById('browse-button');
            const qualitySlider = document.getElementById('quality');
            const qualityValue = document.getElementById('quality-value');
            const formatSelect = document.getElementById('format');
            const maintainDimensions = document.getElementById('maintain-dimensions');
            const previewContainer = document.getElementById('preview-container');
            const imagePreview = document.getElementById('image-preview');
            const resultsContainer = document.getElementById('results-container');
            const compressionResults = document.getElementById('compression-results');
            const downloadAllButton = document.getElementById('download-all');
            const downloadZipButton = document.getElementById('download-zip');
            const loadingOverlay = document.getElementById('loading-overlay');
            const loadingText = document.getElementById('loading-text');

            // Store original and compressed images
            const processedImages = [];

            // Update quality value display
            qualitySlider.addEventListener('input', function() {
                qualityValue.textContent = this.value;
            });

            // Setup file input
            browseButton.addEventListener('click', function() {
                fileInput.click();
            });

            fileInput.addEventListener('change', function() {
                handleFiles(this.files);
            });

            // Setup drag and drop
            ['dragenter', 'dragover', 'dragleave', 'drop'].forEach(eventName => {
                dropArea.addEventListener(eventName, preventDefaults, false);
            });

            function preventDefaults(e) {
                e.preventDefault();
                e.stopPropagation();
            }

            ['dragenter', 'dragover'].forEach(eventName => {
                dropArea.addEventListener(eventName, highlight, false);
            });

            ['dragleave', 'drop'].forEach(eventName => {
                dropArea.addEventListener(eventName, unhighlight, false);
            });

            function highlight() {
                dropArea.classList.add('highlight');
            }

            function unhighlight() {
                dropArea.classList.remove('highlight');
            }

            dropArea.addEventListener('drop', function(e) {
                const dt = e.dataTransfer;
                const files = dt.files;
                handleFiles(files);
            });

            // Handle selected files
            function handleFiles(files) {
                if (files.length === 0) return;
                
                // Clear previous results
                processedImages.length = 0;
                imagePreview.innerHTML = '';
                compressionResults.innerHTML = '';
                
                // Show loading overlay
                loadingOverlay.classList.remove('hidden');
                loadingText.textContent = `Processing ${files.length} image(s)...`;
                
                let processedCount = 0;
                
                Array.from(files).forEach((file, index) => {
                    if (!file.type.match('image.*')) {
                        processedCount++;
                        if (processedCount === files.length) {
                            finishProcessing();
                        }
                        return;
                    }
                    
                    // Read original file for preview and comparison
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        const originalDataUrl = e.target.result;
                        
                        // Compress the image
                        new Compressor(file, {
                            quality: qualitySlider.value / 100,
                            mimeType: formatSelect.value === 'auto' ? file.type : `image/${formatSelect.value}`,
                            maxWidth: maintainDimensions.checked ? undefined : 1920,
                            maxHeight: maintainDimensions.checked ? undefined : 1080,
                            success(compressedBlob) {
                                const reader = new FileReader();
                                reader.onload = function(e) {
                                    const compressedDataUrl = e.target.result;
                                    
                                    // Calculate size savings
                                    const originalSize = file.size;
                                    const compressedSize = compressedBlob.size;
                                    const savings = originalSize - compressedSize;
                                    const savingsPercent = Math.round((savings / originalSize) * 100);
                                    
                                    // Store processed image data
                                    processedImages.push({
                                        originalName: file.name,
                                        originalType: file.type,
                                        originalSize: originalSize,
                                        originalDataUrl: originalDataUrl,
                                        compressedBlob: compressedBlob,
                                        compressedSize: compressedSize,
                                        compressedDataUrl: compressedDataUrl,
                                        savings: savings,
                                        savingsPercent: savingsPercent
                                    });
                                    
                                    // Add to preview
                                    addImagePreview(originalDataUrl, compressedDataUrl, file.name, originalSize, compressedSize, savingsPercent);
                                    
                                    // Add to results
                                    addCompressionResult(file.name, originalSize, compressedSize, savingsPercent, compressedDataUrl, index);
                                    
                                    processedCount++;
                                    if (processedCount === files.length) {
                                        finishProcessing();
                                    }
                                };
                                reader.readAsDataURL(compressedBlob);
                            },
                            error(err) {
                                console.error(err.message);
                                processedCount++;
                                if (processedCount === files.length) {
                                    finishProcessing();
                                }
                            }
                        });
                    };
                    reader.readAsDataURL(file);
                });
            }

            function addImagePreview(originalDataUrl, compressedDataUrl, fileName, originalSize, compressedSize, savingsPercent) {
                const previewDiv = document.createElement('div');
                previewDiv.className = 'grid grid-cols-2 gap-4 border rounded-lg p-4';
                
                // Original image
                const originalDiv = document.createElement('div');
                originalDiv.className = 'flex flex-col items-center';
                const originalImg = document.createElement('img');
                originalImg.src = originalDataUrl;
                originalImg.className = 'preview-img mb-2 rounded';
                const originalTitle = document.createElement('p');
                originalTitle.className = 'font-semibold';
                originalTitle.textContent = 'Original';
                const originalSizeText = document.createElement('p');
                originalSizeText.className = 'text-sm text-gray-600';
                originalSizeText.textContent = formatBytes(originalSize);
                originalDiv.appendChild(originalImg);
                originalDiv.appendChild(originalTitle);
                originalDiv.appendChild(originalSizeText);
                
                // Compressed image
                const compressedDiv = document.createElement('div');
                compressedDiv.className = 'flex flex-col items-center';
                const compressedImg = document.createElement('img');
                compressedImg.src = compressedDataUrl;
                compressedImg.className = 'preview-img mb-2 rounded';
                const compressedTitle = document.createElement('p');
                compressedTitle.className = 'font-semibold';
                compressedTitle.textContent = 'Compressed';
                const compressedSizeText = document.createElement('p');
                compressedSizeText.className = 'text-sm text-gray-600';
                compressedSizeText.textContent = formatBytes(compressedSize) + ` (${savingsPercent}% smaller)`;
                compressedDiv.appendChild(compressedImg);
                compressedDiv.appendChild(compressedTitle);
                compressedDiv.appendChild(compressedSizeText);
                
                previewDiv.appendChild(originalDiv);
                previewDiv.appendChild(compressedDiv);
                imagePreview.appendChild(previewDiv);
            }

            function addCompressionResult(fileName, originalSize, compressedSize, savingsPercent, compressedDataUrl, index) {
                const resultDiv = document.createElement('div');
                resultDiv.className = 'flex justify-between items-center p-4 bg-gray-50 rounded-lg';
                
                const fileInfo = document.createElement('div');
                fileInfo.className = 'flex-1';
                
                const nameElement = document.createElement('p');
                nameElement.className = 'font-semibold';
                nameElement.textContent = fileName;
                
                const statsElement = document.createElement('p');
                statsElement.className = 'text-sm text-gray-600';
                statsElement.innerHTML = `${formatBytes(originalSize)} → ${formatBytes(compressedSize)} <span class="text-green-600 font-medium">(${savingsPercent}% saved)</span>`;
                
                fileInfo.appendChild(nameElement);
                fileInfo.appendChild(statsElement);
                
                const actions = document.createElement('div');
                actions.className = 'flex gap-2';
                
                // Preview button
                const previewButton = document.createElement('button');
                previewButton.className = 'text-blue-600 hover:text-blue-800 p-2';
                previewButton.innerHTML = '<i class="fas fa-eye"></i>';
                previewButton.title = 'Preview';
                previewButton.onclick = function() {
                    const modal = document.createElement('div');
                    modal.className = 'fixed inset-0 flex items-center justify-center bg-black bg-opacity-75 z-50';
                    
                    const modalContent = document.createElement('div');
                    modalContent.className = 'relative bg-white rounded-lg max-w-3xl max-h-[90vh] overflow-auto p-4';
                    
                    const closeButton = document.createElement('button');
                    closeButton.className = 'absolute top-2 right-2 text-gray-500 hover:text-gray-800';
                    closeButton.innerHTML = '<i class="fas fa
