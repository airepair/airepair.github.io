<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Video Enhancer Pro</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        .file-upload {
            border: 2px dashed #ccc;
            transition: all 0.3s;
        }
        .file-upload:hover {
            border-color: #4f46e5;
        }
        .processing-bar {
            transition: width 0.5s ease-in-out;
        }
        .before-after-container {
            perspective: 1000px;
        }
        .before-after-slider {
            transition: transform 0.5s ease-in-out;
        }
        .before-after-slider:hover {
            transform: rotateY(10deg);
        }
    </style>
</head>
<body class="bg-gray-50 min-h-screen">
    <header class="bg-gradient-to-r from-purple-600 to-blue-600 text-white py-8">
        <div class="container mx-auto px-4">
            <div class="flex items-center justify-between">
                <div>
                    <h1 class="text-3xl font-bold">AI Video Enhancer Pro</h1>
                    <p class="opacity-90">Frame interpolation & quality restoration powered by AI</p>
                </div>
                <div class="flex space-x-4">
                    <button class="px-4 py-2 bg-white text-purple-600 rounded-lg font-medium hover:bg-gray-100 transition">Login</button>
                    <button class="px-4 py-2 bg-purple-700 text-white rounded-lg font-medium hover:bg-purple-800 transition">Sign Up</button>
                </div>
            </div>
        </div>
    </header>
    <main class="container mx-auto px-4 py-12">
        <div class="max-w-4xl mx-auto bg-white rounded-xl shadow-lg overflow-hidden">
            <div class="p-8">
                <h2 class="text-2xl font-bold text-gray-800 mb-2">Enhance Your Videos</h2>
                <p class="text-gray-600 mb-6">
                    Upload your video to increase frame rate (up to 60/120fps) and enhance resolution (up to 4K/8K) 
                    using our advanced AI technology.
                </p>
                <!-- Upload Area -->
                <div id="upload-section" class="file-upload bg-gray-50 rounded-lg p-8 text-center mb-8 cursor-pointer">
                    <input type="file" id="video-upload" class="hidden" accept="video/*">
                    <label for="video-upload" class="block">
                        <div class="mx-auto w-16 h-16 bg-purple-100 rounded-full flex items-center justify-center text-purple-600 mb-4">
                            <i class="fas fa-cloud-upload-alt text-2xl"></i>
                        </div>
                        <h3 class="text-lg font-medium text-gray-700 mb-1">Drag & drop your video file here</h3>
                        <p class="text-gray-500 text-sm">or click to browse files (MP4, MOV, AVI up to 2GB)</p>
                    </label>
                </div>
                <!-- Settings -->
                <div id="settings-section" class="hidden mb-8">
                    <h3 class="text-lg font-medium text-gray-800 mb-4">Processing Settings</h3>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-1">Frame Rate Enhancement</label>
                            <select class="w-full border border-gray-300 rounded-md py-2 px-3 focus:outline-none focus:ring-2 focus:ring-purple-500">
                                <option>Original (no change)</option>
                                <option selected>2x Interpolation (30fps → 60fps)</option>
                                <option>4x Interpolation (30fps → 120fps)</option>
                                <option>Custom value...</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-1">Quality Enhancement</label>
                            <select class="w-full border border-gray-300 rounded-md py-2 px-3 focus:outline-none focus:ring-2 focus:ring-purple-500">
                                <option>Original (no change)</option>
                                <option selected>Upscale to 1080p</option>
                                <option>Upscale to 4K</option>
                                <option>Upscale to 8K</option>
                                <option>Fix artifacts & noise</option>
                                <option>All enhancements</option>
                            </select>
                        </div>
                    </div>
                    <button id="start-processing" class="w-full md:w-auto bg-purple-600 hover:bg-purple-700 text-white py-3 px-6 rounded-lg font-medium transition">
                        Start Enhancement Process
                    </button>
                </div>
                <!-- Processing Status -->
                <div id="processing-section" class="hidden mb-8">
                    <h3 class="text-lg font-medium text-gray-800 mb-4">Enhancement Progress</h3>
                    <div class="bg-gray-100 p-4 rounded-lg mb-4">
                        <div class="flex justify-between text-sm text-gray-600 mb-1">
                            <span>Processing...</span>
                            <span id="progress-percent">0%</span>
                        </div>
                        <div class="w-full bg-gray-300 rounded-full h-2.5">
                            <div id="progress-bar" class="processing-bar bg-purple-600 h-2.5 rounded-full" style="width: 0%"></div>
                        </div>
                    </div>
                    <div class="grid grid-cols-2 gap-4 text-sm">
                        <div class="bg-gray-50 p-3 rounded-lg">
                            <div class="text-gray-500 mb-1">Current Task</div>
                            <div id="current-task" class="font-medium">Preparing video analysis</div>
                        </div>
                        <div class="bg-gray-50 p-3 rounded-lg">
                            <div class="text-gray-500 mb-1">Time Remaining</div>
                            <div id="time-remaining" class="font-medium">Calculating...</div>
                        </div>
                    </div>
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/473daaf2-698d-404d-afe4-65c33eac55c2.png" alt="AI neural network processing visualization with interconnected nodes and data flowing through them" class="mt-6 rounded-lg w-full" />
                </div>
                <!-- Results Section -->
                <div id="results-section" class="hidden">
                    <div class="flex justify-between items-center mb-4">
                        <h3 class="text-lg font-medium text-gray-800">Enhancement Results</h3>
                        <div class="bg-green-100 text-green-800 text-sm px-3 py-1 rounded-full">
                            <i class="fas fa-check-circle mr-1"></i> Completed
                        </div>
                    </div>
                    <div class="before-after-container bg-gray-100 p-6 rounded-xl mb-6">
                        <div class="relative before-after-slider overflow-hidden rounded-lg">
                            <div class="aspect-w-16 aspect-h-9 relative">
                                <div class="relative pb-[56.25%]">
                                    <div id="before-video-placeholder" class="absolute inset-0 bg-gray-300 flex items-center justify-center">
                                        <div class="text-center">
                                            <i class="fas fa-film text-4xl text-gray-500 mb-2"></i>
                                            <p class="text-gray-600">Original Video Preview</p>
                                        </div>
                                    </div>
                                    <div id="after-video-placeholder" class="absolute inset-0 bg-gray-200 flex items-center justify-center">
                                        <div class="text-center">
                                            <i class="fas fa-magic text-4xl text-purple-500 mb-2"></i>
                                            <p class="text-gray-600">Enhanced Video Preview</p>
                                        </div>
                                    </div>
                                </div>
                                <div class="absolute top-0 left-0 right-0 h-full w-1/2 bg-blue-200 opacity-30 border-r-2 border-white z-10 cursor-col-resize"></div>
                            </div>
                        </div>
                        <div class="flex justify-between mt-2 text-sm text-gray-600">
                            <span>Before</span>
                            <span>After</span>
                        </div>
                    </div>
                    <div class="grid md:grid-cols-2 gap-6">
                        <div class="bg-gray-50 p-5 rounded-lg">
                            <h4 class="font-medium text-gray-800 mb-3">Original Video</h4>
                            <ul class="space-y-2 text-sm text-gray-600">
                                <li class="flex"><span class="w-32">Resolution:</span> <span id="original-resolution" class="font-medium">720p</span></li>
                                <li class="flex"><span class="w-32">Frame Rate:</span> <span id="original-fps" class="font-medium">30fps</span></li>
                                <li class="flex"><span class="w-32">Duration:</span> <span id="original-duration" class="font-medium">00:02:15</span></li>
                                <li class="flex"><span class="w-32">File Size:</span> <span id="original-size" class="font-medium">45.3MB</span></li>
                            </ul>
                        </div>
                        <div class="bg-purple-50 p-5 rounded-lg">
                            <h4 class="font-medium text-gray-800 mb-3">
                                Enhanced Results
                                <span class="ml-2 bg-purple-100 text-purple-800 text-xs px-2 py-0.5 rounded">AI Processed</span>
                            </h4>
                            <ul class="space-y-2 text-sm text-gray-600">
                                <li class="flex"><span class="w-32">Resolution:</span> <span id="enhanced-resolution" class="font-medium">1080p</span></li>
                                <li class="flex"><span class="w-32">Frame Rate:</span> <span id="enhanced-fps" class="font-medium">60fps</span></li>
                                <li class="flex"><span class="w-32">Duration:</span> <span id="enhanced-duration" class="font-medium">00:02:15</span></li>
                                <li class="flex"><span class="w-32">File Size:</span> <span id="enhanced-size" class="font-medium">127.8MB</span></li>
                            </ul>
                        </div>
                    </div>
                    <div class="mt-6 flex flex-col sm:flex-row justify-center gap-4">
                        <button id="download-btn" class="bg-purple-600 hover:bg-purple-700 text-white py-3 px-6 rounded-lg font-medium transition flex items-center justify-center">
                            <i class="fas fa-download mr-2"></i> Download Enhanced Video
                        </button>
                        <button id="new-upload-btn" class="bg-white border border-gray-300 hover:bg-gray-50 text-gray-700 py-3 px-6 rounded-lg font-medium transition">
                            Process Another Video
                        </button>
                    </div>
                </div>
            </div>
            <div class="bg-gray-50 px-8 py-6 border-t border-gray-200">
                <h3 class="text-lg font-medium text-gray-800 mb-3">How It Works</h3>
                <div class="grid md:grid-cols-3 gap-6">
                    <div class="flex items-start">
                        <div class="bg-purple-100 text-purple-600 rounded-full w-10 h-10 flex items-center justify-center mr-3 flex-shrink-0">
                            <i class="fas fa-upload"></i>
                        </div>
                        <div>
                            <h4 class="font-medium text-gray-800">Upload Your Video</h4>
                            <p class="text-gray-600 text-sm mt-1">Drag and drop your video file or click to browse your files.</p>
                        </div>
                    </div>
                    <div class="flex items-start">
                        <div class="bg-purple-100 text-purple-600 rounded-full w-10 h-10 flex items-center justify-center mr-3 flex-shrink-0">
                            <i class="fas fa-cogs"></i>
                        </div>
                        <div>
                            <h4 class="font-medium text-gray-800">AI Processing</h4>
                            <p class="text-gray-600 text-sm mt-1">Our technology analyzes and enhances each frame using neural networks.</p>
                        </div>
                    </div>
                    <div class="flex items-start">
                        <div class="bg-purple-100 text-purple-600 rounded-full w-10 h-10 flex items-center justify-center mr-3 flex-shrink-0">
                            <i class="fas fa-download"></i>
                        </div>
                        <div>
                            <h4 class="font-medium text-gray-800">Download Results</h4>
                            <p class="text-gray-600 text-sm mt-1">Get your enhanced video with improved frame rate and resolution.</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="mt-8 bg-white rounded-xl shadow-lg overflow-hidden">
            <div class="p-6">
                <h3 class="text-lg font-medium text-gray-800 mb-3">Sample Comparisons</h3>
                <p class="text-gray-600 mb-4">See what our AI enhancement can do for your videos.</p>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
                    <div class="border border-gray-200 rounded-lg overflow-hidden">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/c91c4e2d-a351-4044-bd3c-ad6fa2a30c64.png" alt="Comparison of low-quality CCTV footage left side and AI-enhanced high-definition version on the right" class="w-full" />
                        <div class="p-3">
                            <h4 class="font-medium text-gray-800">Security Footage</h4>
                            <p class="text-gray-600 text-sm">480p → 1080p enhancement</p>
                        </div>
                    </div>
                    <div class="border border-gray-200 rounded-lg overflow-hidden">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/a3c8baf4-6b1f-468f-a6a7-3c9ef74609ec.png" alt="Old home movie comparison showing grainy film on left and cleaned up digital version on right" class="w-full" />
                        <div class="p-3">
                            <h4 class="font-medium text-gray-800">Home Movies</h4>
                            <p class="text-gray-600 text-sm">8mm film restoration</p>
                        </div>
                    </div>
                    <div class="border border-gray-200 rounded-lg overflow-hidden">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/7438a0ca-1816-40eb-b138-859c43d1b227.png" alt="Sports clip comparison showing motion blur on left and crisp 60fps version on right" class="w-full" />
                        <div class="p-3">
                            <h4 class="font-medium text-gray-800">Sports Videos</h4>
                            <p class="text-gray-600 text-sm">30fps → 60fps interpolation</p>
                        </div>
                    </div>
                    <div class="border border-gray-200 rounded-lg overflow-hidden">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/ef3e6ccd-9e2e-4cb5-9f36-4712d1db0b56.png" alt="Anime comparison showing compressed version left and AI-upscaled crisp version right" class="w-full" />
                        <div class="p-3">
                            <h4 class="font-medium text-gray-800">Animation</h4>
                            <p class="text-gray-600 text-sm">Resolution enhancement</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </main>
    <footer class="bg-gray-800 text-white py-8">
        <div class="container mx-auto px-4">
            <div class="grid md:grid-cols-4 gap-8">
                <div>
                    <h4 class="text-lg font-medium mb-4">AI Video Enhancer Pro</h4>
                    <p class="text-gray-400 text-sm">Professional quality video enhancement powered by artificial intelligence.</p>
                </div>
                <div>
                    <h4 class="text-lg font-medium mb-4">Features</h4>
                    <ul class="space-y-2 text-gray-400 text-sm">
                        <li><a href="#" class="hover:text-white transition">Frame Interpolation</a></li>
                        <li><a href="#" class="hover:text-white transition">Quality Enhancement</a></li>
                        <li><a href="#" class="hover:text-white transition">Noise Reduction</a></li>
                        <li><a href="#" class="hover:text-white transition">Color Correction</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="text-lg font-medium mb-4">Resources</h4>
                    <ul class="space-y-2 text-gray-400 text-sm">
                        <li><a href="#" class="hover:text-white transition">Documentation</a></li>
                        <li><a href="#" class="hover:text-white transition">API Reference</a></li>
                        <li><a href="#" class="hover:text-white transition">Pricing</a></li>
                        <li><a href="#" class="hover:text-white transition">FAQ</a></li>
                    </ul>
                </div>
                <div>
                    <h4 class="text-lg font-medium mb-4">Legal</h4>
                    <ul class="space-y-2 text-gray-400 text-sm">
                        <li><a href="#" class="hover:text-white transition">Terms of Service</a></li>
                        <li><a href="#" class="hover:text-white transition">Privacy Policy</a></li>
                        <li><a href="#" class="hover:text-white transition">Cookie Policy</a></li>
                    </ul>
                </div>
            </div>
            <div class="border-t border-gray-700 mt-8 pt-8 text-center text-gray-400 text-sm">
                <p>© 2023 AI Video Enhancer Pro. All rights reserved.</p>
            </div>
        </div>
    </footer>
    <script>
        // File Upload Handler
        document.getElementById('video-upload').addEventListener('change', function(e) {
            const file = e.target.files[0];
            if (file) {
                // Validate file type
                const validTypes = ['video/mp4', 'video/quicktime', 'video/x-msvideo'];
                if (!validTypes.includes(file.type)) {
                    alert('Please upload a valid video file (MP4, MOV, or AVI)');
                    return;
                }
                
               
