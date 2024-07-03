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

simple modal
```js
import React from 'react';
import { GoX } from "react-icons/go";

const ProjectDetailModal = () => {
    return (
        <div className='fixed inset-0 bg-black bg-opacity-15 flex items-center justify-center z-50'>
            <div className='bg-base-100 md:w-[80vw] w-full max-h-[90vh] h-full rounded-lg flex flex-col'>
                <div className='bg-secondary w-full rounded-t-lg flex justify-between'>
                    <div></div>
                    <button className='btn btn-ghost btn-square'><GoX size={30} /></button>
                </div>
                <div className='p-6 flex-1  overflow-y-auto'>
                    <h3>Lorem ipsum dolor sit.</h3>
                    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Iusto ullam minus sapiente consequatur hic sed, saepe rem praesentium. Nihil ex voluptate voluptates nisi necessitatibus soluta expedita quasi in deserunt ratione.</p>
                    Lorem ipsum dolor sit amet consectetur adipisicing elit. Optio veniam, animi tempore quisquam quod dicta aut perspiciatis, libero, maxime tenetur odit vitae molestiae eius nobis doloribus facilis deleniti saepe natus recusandae voluptate? Perferendis sequi quo tempore nulla consequuntur, ex reiciendis, laudantium a adipisci pariatur quisquam ullam soluta quos. Quos laboriosam qui, necessitatibus nam enim optio eos minima at eius inventore, cumque sunt quae porro officia. Deserunt cupiditate eum officiis voluptatibus? Earum sapiente odit molestiae eius dolorem, porro quia, veniam incidunt at recusandae ea quibusdam. Temporibus veritatis nam eveniet dolore debitis! Optio accusamus dolor adipisci alias necessitatibus ullam expedita ipsa? Quidem veniam, accusantium, fugit sequi nulla non rerum earum a tenetur eligendi voluptatem sunt perferendis numquam. Fuga placeat quod, a mollitia odit obcaecati omnis sit officiis inventore possimus dignissimos sunt itaque hic tempore, aliquam nihil sint blanditiis quam. Accusantium eveniet incidunt, quibusdam temporibus qui provident aliquam obcaecati maiores quia voluptatum. Quaerat tenetur eos atque animi est ipsa repudiandae officia delectus repellendus excepturi, incidunt eius sapiente necessitatibus labore nostrum minus earum, quisquam quia, nobis temporibus magni fuga fugiat nemo. Veritatis error voluptatum architecto facere et, incidunt odio. Minima veritatis impedit doloremque culpa perferendis error accusamus vero inventore itaque, earum, quo unde. Quaerat non consectetur totam iure minima voluptatum magnam explicabo commodi at natus, pariatur delectus nemo eos velit nam, vitae, dignissimos quae dicta veritatis molestias. Nesciunt qui nulla repellendus porro. Natus molestias amet ipsam iure facilis mollitia vero non? Explicabo, expedita enim incidunt architecto placeat natus sint veniam repellendus maxime consectetur totam recusandae quo sapiente quam temporibus obcaecati veritatis corrupti ex, id officiis neque numquam. Placeat, vitae eos aliquid fuga a optio repellendus hic voluptas facilis. Nostrum facere incidunt quas provident reiciendis ut autem, molestias quasi tenetur optio tempore beatae blanditiis nobis? Tenetur eveniet officiis debitis nisi neque facilis ab! Repellendus, harum. Expedita ducimus ratione nulla placeat error praesentium tempore, aut nesciunt nihil iste asperiores voluptatem possimus culpa corporis minus aspernatur ab dolorem assumenda esse blanditiis libero, at repudiandae. Nemo sunt eligendi velit unde nobis rerum totam molestias neque. Quibusdam et facere ea unde praesentium, explicabo beatae, quod, id sit iste eius voluptatum ipsam incidunt reprehenderit alias hic earum animi obcaecati nisi fugiat dolor eveniet quae similique. Eius sed perspiciatis alias sunt iusto saepe tempora deserunt molestias fugiat excepturi impedit, perferendis quae culpa, cupiditate maxime odit. Sapiente quae distinctio, quo temporibus modi molestias illum rem dolorem ullam accusamus deleniti accusantium consequuntur libero, vero voluptas labore impedit aperiam sequi! Harum vero error omnis vitae voluptate animi similique explicabo, doloremque, facilis illo rem suscipit alias placeat dolores. Maxime cum, doloribus totam consequatur est porro. Itaque pariatur earum voluptas adipisci, non a hic praesentium nesciunt consectetur soluta voluptates ullam, minima saepe officiis quos voluptatibus! Suscipit quo adipisci odio aut laudantium sequi, fugiat delectus non ut mollitia cum consectetur corporis sunt hic omnis officiis quos ad, ullam praesentium. Temporibus error sint quidem laudantium illum deserunt impedit aut reprehenderit nostrum, harum ex placeat dolor eius. Sint sit quos alias ut dicta inventore dolore illo laudantium, voluptatem earum.
                </div>

            </div>
        </div>
    );
};

export default ProjectDetailModal;
```
