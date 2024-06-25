<script setup lang="ts">
import { ref, onMounted, h } from "vue"
import { useRouter } from "vue-router"
import { useApi } from "@/composables/useApi"
import {t} from "@/i18n"

const api = useApi()
const router = useRouter()
const notification = useNotification();

const deleteMyBook = async (id: number) => {
    api.delete(`http://localhost:3001/book/${id}`).then((response) => {
        notification.success({
            duration: 5000,
            content: "Books",
            meta: response.data.message,
        })
        data.value.splice(
            data.value.findIndex((e) => e.id === id),
            1
        );
    })
}

// id|title   |description   |thumbnail      |author   |created_at         |updated_at         |userId

const columns = [
    {
        type: "selection",
    },
    {
        title: t("books.table.title"),
        key: "title",
        sorter: "default",
    },
    {
        title: t("books.table.description"),
        key: "description",
        sorter: "default",
    },
    {
        title: t("books.table.author"),
        key: "author",
        sorter: "default",
    },
    {
        title: t("books.table.created_at"),
        key: "created_at",
        sorter: "default",
    },
    {
        title: t("books.table.updated_at"),
        key: "updated_at",
        sorter: "default",
    },
    {
        title: t("books.table.actions"),
        key: "actions",
        render(row) {
            return [
                h(
                    NButton,
                    {
                        circle: true,
                        quaternary: true,
                        onClick: () =>
                            router.push({ name: "users.edit", params: { id: row.id } }),
                        icon: () => h(Icon, { name: "edit" }),
                    },
                    { default: () => t("users.table.edit") }
                ),
                h(
                    NButton,
                    {
                        circle: true,
                        quaternary: true,
                        onClick: () => deleteMyBook(row.id),
                        icon: () => h(Icon, { name: "delete" }),
                    },
                    { default: () => t("users.table.delete") }
                ),
            ]
        },
    },
]

