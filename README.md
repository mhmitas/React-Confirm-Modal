# React-Confirm-Modal

confirm.js
```js
import React from 'react';
import { createRoot } from 'react-dom/client';
import ConfirmModal from './ConfirmModal';

const confirm = (message) => {
    return new Promise((resolve, reject) => {
        const div = document.createElement('div');
        document.body.appendChild(div);

        const root = createRoot(div);

        const handleConfirm = () => {
            cleanup();
            resolve(true);
        };

        const handleCancel = () => {
            cleanup();
            resolve(false);
        };

        const cleanup = () => {
            root.unmount();
            div.remove();
        };

        root.render(
            <ConfirmModal
                message={message}
                onConfirm={handleConfirm}
                onCancel={handleCancel}
            />
        );
    });
};

export default confirm;
```
ConfirmModal.js
```js
import React from 'react';

const ConfirmModal = ({ message, onConfirm, onCancel }) => {
    const handleOverlayClick = (e) => {
        if (e.target === e.currentTarget) {
            onCancel();
        }
    };

    return (
        <div
            className="fixed inset-0 flex items-center justify-center bg-gray-800 bg-opacity-75 z-50"
            onClick={handleOverlayClick}
        >
            <div className="bg-white text-slate-950 rounded-lg shadow-lg p-6 w-96">
                <h2 className="mb-2">Confirm Action</h2>
                <p className="text-lg font-semibold mb-6">{message}</p>
                <div className="flex justify-end space-x-4">
                    <button className="bg-blue-500 text-white font-bold py-2 px-4 rounded transition-transform transform hover:bg-blue-600 active:scale-95" onClick={onConfirm}>
                        Confirm
                    </button>
                    <button className="bg-rose-500 text-white font-bold py-2 px-4 rounded transition-transform transform hover:bg-rose-600 active:scale-95" onClick={onCancel}>
                        Cancel
                    </button>
                </div>
            </div>
        </div>
    );
};

export default ConfirmModal;
```


ConfirmModal.js  [animated]
```js
import React, { useState, useEffect } from 'react';

const ConfirmModal = ({ message, onConfirm, onCancel }) => {
    const [isVisible, setIsVisible] = useState(false);

    useEffect(() => {
        // Trigger the visibility change with a slight delay for the fade-in effect
        const timer = setTimeout(() => setIsVisible(true), 10);
        return () => clearTimeout(timer);
    }, []);

    const handleOverlayClick = (e) => {
        if (e.target === e.currentTarget) {
            setIsVisible(false);
            setTimeout(() => onCancel(), 300); // Delay onCancel to allow fade-out effect
        }
    };

    const handleConfirmClick = () => {
        setIsVisible(false);
        setTimeout(() => onConfirm(), 300); // Delay onConfirm to allow fade-out effect
    };

    return (
        <div
            className={`fixed inset-0 flex items-center justify-center bg-gray-800 bg-opacity-55 z-50 transition-opacity duration-300 ${isVisible ? 'opacity-100' : 'opacity-0'}`}
            onClick={handleOverlayClick}
        >
            <div className={`bg-white text-slate-950 rounded-lg shadow-lg p-6 w-96 transform transition-transform duration-300 ${isVisible ? 'scale-100' : 'scale-95'}`}>
                <h2 className="mb-2">Confirm Action</h2>
                <p className="text-xl font-semibold mb-6">{message}</p>
                <div className="flex justify-center space-x-4">
                    <button className="bg-blue-500 text-white font-bold py-2 px-4 rounded transition-transform transform hover:bg-blue-600 active:scale-95" onClick={handleConfirmClick}>
                        Confirm
                    </button>
                    <button className="bg-rose-500 text-white font-bold py-2 px-4 rounded transition-transform transform hover:bg-rose-600 active:scale-95" onClick={handleOverlayClick}>
                        Cancel
                    </button>
                </div>
            </div>
        </div>
    );
};

export default ConfirmModal;
```
