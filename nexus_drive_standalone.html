<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>NEXUS DRIVE — Standalone</title>
  <script src="https://unpkg.com/react@18/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <!-- Tailwind Play CDN for quick styling (not for production) -->
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    @keyframes blob { 0%,100%{transform:translate(0,0) scale(1);}33%{transform:translate(30px,-50px) scale(1.1);}66%{transform:translate(-20px,20px) scale(0.9);} }
    .animate-blob{animation:blob 7s infinite}
    .glass{background:rgba(255,255,255,0.04);backdrop-filter:blur(12px);border:1px solid rgba(255,255,255,0.06)}
    .glow{box-shadow:0 6px 30px rgba(139,92,246,0.12)}
  </style>
</head>
<body class="bg-black text-white min-h-screen">
  <div id="root"></div>

  <script type="text/babel">
    const { useState, useEffect } = React;

    function Icon({ name }){
      // tiny icon helper (returns simple SVGs)
      const common = { width: 20, height: 20 };
      if(name === 'folder') return (<svg {...common} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5"><path d="M3 7v13a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V9a2 2 0 0 0-2-2H12l-2-2H5a2 2 0 0 0-2 2z"/></svg>);
      if(name === 'upload') return (<svg {...common} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5"><path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/><path d="M7 10l5-5 5 5"/><path d="M12 5v14"/></svg>);
      if(name === 'search') return (<svg {...common} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5"><circle cx="11" cy="11" r="6"/><path d="M21 21l-4.35-4.35"/></svg>);
      if(name === 'file') return (<svg {...common} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><path d="M14 2v6h6"/></svg>);
      if(name === 'trash') return (<svg {...common} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5"><polyline points="3 6 5 6 21 6"/><path d="M19 6l-1 14a2 2 0 0 1-2 2H8a2 2 0 0 1-2-2L5 6"/><path d="M10 11v6"/><path d="M14 11v6"/><path d="M9 6V4a2 2 0 0 1 2-2h2a2 2 0 0 1 2 2v2"/></svg>);
      return null;
    }

    function App(){
      const [files, setFiles] = useState([]);
      const [folders, setFolders] = useState([{ id: 'root', name: 'Home', parent: null }]);
      const [currentFolder, setCurrentFolder] = useState('root');
      const [viewMode, setViewMode] = useState('grid');
      const [searchQuery, setSearchQuery] = useState('');
      const [filterType, setFilterType] = useState('all');
      const [showNewFolderModal, setShowNewFolderModal] = useState(false);
      const [newFolderName, setNewFolderName] = useState('');
      const [sortBy, setSortBy] = useState('name');
      const [isDragging, setIsDragging] = useState(false);
      const [uploadProgress, setUploadProgress] = useState(0);

      useEffect(()=>{ loadData(); }, []);

      function loadData(){
        try{
          const f = localStorage.getItem('nexus_files');
          const d = localStorage.getItem('nexus_folders');
          if(f) setFiles(JSON.parse(f));
          if(d) setFolders(JSON.parse(d));
        }catch(e){ console.warn('load error', e); }
      }

      function saveData(nextFiles, nextFolders){
        try{
          localStorage.setItem('nexus_files', JSON.stringify(nextFiles));
          localStorage.setItem('nexus_folders', JSON.stringify(nextFolders));
        }catch(e){ console.warn('save error', e); }
      }

      const handleFileUpload = (uploadedFiles) => {
        if(!uploadedFiles || uploadedFiles.length===0) return;
        setUploadProgress(20);
        const arr = Array.from(uploadedFiles).map(file => ({
          id: Date.now() + Math.random(),
          name: file.name,
          type: file.type || 'application/octet-stream',
          size: file.size || 0,
          folder: currentFolder,
          uploadDate: new Date().toISOString(),
          data: URL.createObjectURL(file)
        }));
        setTimeout(()=>{
          const updated = [...files, ...arr];
          setFiles(updated);
          saveData(updated, folders);
          setUploadProgress(100);
          setTimeout(()=>setUploadProgress(0), 500);
        }, 250);
      };

      const handleDrop = (e) => { e.preventDefault(); setIsDragging(false); if(e.dataTransfer && e.dataTransfer.files) handleFileUpload(e.dataTransfer.files); };

      const createFolder = () => {
        if(!newFolderName.trim()) return;
        const newF = { id: Date.now().toString(), name: newFolderName.trim(), parent: currentFolder };
        const updated = [...folders, newF];
        setFolders(updated);
        saveData(files, updated);
        setNewFolderName(''); setShowNewFolderModal(false);
      };

      const deleteFile = (id)=>{ const updated = files.filter(f=>f.id!==id); setFiles(updated); saveData(updated, folders); };

      const deleteFolder = (id)=>{
        if(id==='root') return;
        const updatedFolders = folders.filter(f=>f.id!==id && f.parent!==id);
        const updatedFiles = files.filter(f=>f.folder!==id);
        setFolders(updatedFolders); setFiles(updatedFiles); saveData(updatedFiles, updatedFolders);
        if(currentFolder===id){ const found = folders.find(f=>f.id===id); setCurrentFolder(found?.parent||'root'); }
      };

      const getCurrentFolderPath = ()=>{
        const path=[]; let cur=currentFolder; while(cur){ const folder=folders.find(f=>f.id===cur); if(folder){ path.unshift(folder); cur=folder.parent; } else break; } return path;
      };

      const getFilteredAndSortedItems = ()=>{
        const currentFolders = folders.filter(f=>f.parent===currentFolder);
        let currentFiles = files.filter(f=>f.folder===currentFolder);
        if(searchQuery) currentFiles = currentFiles.filter(f=>f.name.toLowerCase().includes(searchQuery.toLowerCase()));
        if(filterType!=='all') currentFiles = currentFiles.filter(f=>f.type.startsWith(filterType+'/'));
        currentFiles.sort((a,b)=>{ if(sortBy==='name') return a.name.localeCompare(b.name); if(sortBy==='date') return new Date(b.uploadDate)-new Date(a.uploadDate); if(sortBy==='size') return b.size-a.size; return 0; });
        return { currentFolders, currentFiles };
      };

      const formatFileSize = (bytes)=>{ if(!bytes) return '0 B'; const k=1024; const sizes=['B','KB','MB','GB']; const i=Math.floor(Math.log(bytes)/Math.log(k)); return Math.round(bytes/Math.pow(k,i)*100)/100 + ' ' + sizes[i]; };

      const { currentFolders, currentFiles } = getFilteredAndSortedItems();
      const path = getCurrentFolderPath();
      const totalFiles = files.length;
      const totalSize = files.reduce((s,f)=>s+ (f.size||0),0);

      return (
        <div className="relative z-10 max-w-6xl mx-auto p-6">
          <div className="glass rounded-2xl p-6 mb-6 glow">
            <div className="flex items-center justify-between mb-4">
              <div>
                <div className="flex items-center gap-3 mb-2">
                  <div className="bg-gradient-to-r from-purple-500 to-cyan-500 p-3 rounded-2xl">
                    <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="white" strokeWidth="1.5"><path d="M12 2v6l4 4"/></svg>
                  </div>
                  <div>
                    <h1 className="text-2xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-purple-400 to-cyan-400">NEXUS DRIVE</h1>
                    <p className="text-gray-300 text-sm">{totalFiles} files • {formatFileSize(totalSize)}</p>
                  </div>
                </div>
              </div>
              <div className="flex gap-3">
                <button onClick={()=>setShowNewFolderModal(true)} className="flex items-center gap-2 bg-purple-600 px-4 py-2 rounded-lg">📁 New Folder</button>
                <label className="flex items-center gap-2 bg-cyan-600 px-4 py-2 rounded-lg cursor-pointer">
                  ⬆️ Upload
                  <input type="file" multiple onChange={(e)=>handleFileUpload(e.target.files)} className="hidden" />
                </label>
              </div>
            </div>

            {uploadProgress>0 && (<div className="mb-4"><div className="h-2 bg-gray-800 rounded-full overflow-hidden"><div style={{width: uploadProgress+'%'}} className="h-full bg-gradient-to-r from-cyan-400 to-purple-500"></div></div></div>)}

            <div className="flex items-center gap-2 mb-4 text-gray-400">
              {path.map((p, i)=> (<React.Fragment key={p.id}><button onClick={()=>setCurrentFolder(p.id)} className="hover:text-cyan-300">{p.name}</button>{i<path.length-1 && <span className="text-gray-600">/</span>}</React.Fragment>))}
            </div>

            <div className="flex flex-wrap gap-3">
              <div className="flex-1 min-w-[200px] relative">
                <span style={{position:'absolute',left:12,top:10}}><Icon name="search" /></span>
                <input value={searchQuery} onChange={(e)=>setSearchQuery(e.target.value)} placeholder="Search files..." className="w-full pl-10 pr-4 py-2 bg-white/5 rounded-lg" />
              </div>

              <select value={filterType} onChange={(e)=>setFilterType(e.target.value)} className="px-3 py-2 bg-white/5 rounded-lg">
                <option value="all">All Types</option>
                <option value="image">Images</option>
                <option value="video">Videos</option>
                <option value="audio">Audio</option>
                <option value="application">Documents</option>
              </select>

              <select value={sortBy} onChange={(e)=>setSortBy(e.target.value)} className="px-3 py-2 bg-white/5 rounded-lg">
                <option value="name">Name</option>
                <option value="date">Date</option>
                <option value="size">Size</option>
              </select>

              <div className="flex gap-2">
                <button onClick={()=>setViewMode('grid')} className={`px-3 py-2 rounded-lg ${viewMode==='grid'?'bg-purple-600':''}`}>Grid</button>
                <button onClick={()=>setViewMode('list')} className={`px-3 py-2 rounded-lg ${viewMode==='list'?'bg-purple-600':''}`}>List</button>
              </div>
            </div>
          </div>

          <div onDragOver={(e)=>{e.preventDefault(); setIsDragging(true);}} onDragLeave={()=>setIsDragging(false)} onDrop={handleDrop} className={`glass rounded-2xl p-6 transition ${isDragging? 'border-2 border-cyan-500 bg-cyan-600/10':''}`}>
            {isDragging && (<div className="text-center py-8 mb-4 border-2 border-dashed border-cyan-500 rounded-lg"><div className="text-cyan-400 text-xl">Drop files here</div></div>)}

            {currentFolders.length===0 && currentFiles.length===0 ? (
              <div className="text-center py-16"><div className="w-20 h-20 rounded-full bg-gradient-to-r from-purple-500 to-cyan-500 mx-auto mb-4 flex items-center justify-center">📁</div><div className="text-lg font-bold">No files yet</div><div className="text-gray-400">Upload files or create a folder</div></div>
            ) : (
              <>
                {currentFolders.length>0 && (<div className="mb-6"><h3 className="text-sm text-gray-400 mb-3">Folders</h3><div className={viewMode==='grid'? 'grid grid-cols-2 md:grid-cols-4 gap-4':'space-y-2'}>{currentFolders.map(folder=> (
                  <div key={folder.id} className="glass p-4 rounded-lg hover:bg-white/5 cursor-pointer group" onDoubleClick={()=>setCurrentFolder(folder.id)}>
                    <div className="text-center"><div className="w-16 h-16 rounded-lg bg-yellow-400/30 mx-auto mb-3 flex items-center justify-center">📁</div><div className="font-medium truncate">{folder.name}</div></div>
                    {folder.id!=='root' && (<button onClick={(e)=>{e.stopPropagation(); deleteFolder(folder.id);}} className="mt-2 text-sm text-red-400">Delete</button>)}
                  </div>
                ))}</div></div>)}

                {currentFiles.length>0 && (<div><h3 className="text-sm text-gray-400 mb-3">Files</h3><div className={viewMode==='grid'? 'grid grid-cols-2 md:grid-cols-4 gap-4':'space-y-2'}>{currentFiles.map(file=> (
                  <div key={file.id} className="glass p-4 rounded-lg group relative">
                    <div className="text-center">
                      {file.type.startsWith('image/') ? (
                        <img src={file.data} alt={file.name} style={{width:'100%', height:120, objectFit:'cover'}} className="rounded-md mb-2" />
                      ) : (
                        <div className="w-16 h-16 rounded-lg bg-gradient-to-r from-purple-500 to-pink-500 mx-auto mb-2 flex items-center justify-center">{file.type.split('/')[0]||'FILE'}</div>
                      )}
                      <div className="font-medium truncate">{file.name}</div>
                      <div className="text-xs text-gray-400">{formatFileSize(file.size)}</div>
                    </div>
                    <div style={{position:'absolute',right:8,top:8,display:'flex',gap:6}}>
                      <a href={file.data} download={file.name} className="px-2 py-1 bg-cyan-500 rounded">Download</a>
                      <button onClick={()=>deleteFile(file.id)} className="px-2 py-1 bg-red-500 rounded">Delete</button>
                    </div>
                  </div>
                ))}</div></div>)}
              </>
            )}
          </div>

          {showNewFolderModal && (
            <div className="fixed inset-0 bg-black/70 flex items-center justify-center p-4 z-40">
              <div className="glass rounded-2xl p-6 max-w-md w-full">
                <div className="flex items-center justify-between mb-4"><h3 className="text-xl font-bold">Create Folder</h3><button onClick={()=>setShowNewFolderModal(false)}>✖️</button></div>
                <input autoFocus value={newFolderName} onChange={(e)=>setNewFolderName(e.target.value)} onKeyDown={(e)=>e.key==='Enter'&&createFolder()} placeholder="Folder name" className="w-full px-3 py-2 bg-white/5 rounded mb-4" />
                <div className="flex gap-3"><button onClick={()=>setShowNewFolderModal(false)} className="flex-1 px-3 py-2 bg-white/5 rounded">Cancel</button><button onClick={createFolder} className="flex-1 px-3 py-2 bg-purple-600 rounded">Create</button></div>
              </div>
            </div>
          )}
        </div>
      );
    }

    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<App />);
  </script>
</body>
</html>
